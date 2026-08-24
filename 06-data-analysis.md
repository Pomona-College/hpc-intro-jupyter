---
title: 'Data Analysis in Notebooks'
teaching: 25
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I explore and summarize data in a notebook?
- How do I select, filter, and modify data with pandas?
- How do I work with data stored on Sagehen?
- How do I keep a notebook reproducible as analysis grows?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explore datasets using pandas summary methods
- Select, filter, and transform data
- Modify DataFrames with new columns, sorting, and deduplication
- Work with data on Sagehen's storage systems
- Apply notebook hygiene that keeps analysis reproducible

::::::::::::::::::::::::::::::::::::::::::::::

## Why Data Analysis in Notebooks Matters for HPC

Most HPC research starts with a dataset and an investigator who needs to figure out what is in it before deciding how to scale the analysis. Notebooks shine in this exploratory phase because the unit of work is one cell at a time: load, look, plot, decide, adjust. The friction of switching between code and inspection is gone, which means more experiments per hour and faster discovery of the surprises that always live in real data.

The patterns in this episode are equally useful at the small scale (a 100 MB CSV in a notebook on the login node) and the large scale (a 50 GB Parquet dataset that drives a SLURM training job later). Learning them in the notebook context first means you bring the same vocabulary to the cluster.

## Exploring Data

Once you have loaded a dataset, the first hour of any analysis is exploration. Pandas exposes a small vocabulary that, used in order, will tell you almost everything you need to know about a new dataset:

```python
import pandas as pd

df = pd.read_csv('data.csv')

# First rows
print(df.head(10))

# Last rows
print(df.tail())

# Data types
print(df.dtypes)

# Missing values
print(df.isnull().sum())

# Unique values in a column
print(df['category'].unique())

# Value counts
print(df['category'].value_counts())

# Statistics by group
print(df.groupby('category')['value'].mean())

# Correlation matrix
print(df.corr())
```

A useful habit: in your first cell after loading, always print `df.shape`, `df.dtypes`, and `df.isnull().sum()`. The shape tells you whether the load worked. The dtypes catch the most common pandas surprise (numeric column read as object because of one row with stray text). The null count tells you whether to plan for missing-value handling before any analysis.

::::::::::::::::::::::::::::::::::::: callout

## When pandas hits its limits on Sagehen

The login node has plenty of memory for most pandas work, but it is shared with every other user. A 20 GB DataFrame load on the login node hurts everyone. Two thresholds to remember:

If the file is under ~2 GB, load it directly in your login-node notebook.

If the file is between 2 and 50 GB, launch your Jupyter session inside an interactive SLURM allocation: `srun --partition=short --time=02:00:00 --mem=64G --pty bash`, then start jupyter from there.

If the file is over 50 GB, switch to Dask (covered in Workshop 17). Pandas will not fit it in memory.

::::::::::::::::::::::::::::::::::::::::::::::::

## Selecting Data

```python
# Select a column
ages = df['age']

# Select multiple columns
subset = df[['name', 'age', 'salary']]

# Filter rows (age > 25)
young_workers = df[df['age'] > 25]

# Filter multiple conditions
expensive_experienced = df[(df['salary'] > 50000) & (df['age'] > 30)]

# Select by position
first_row = df.iloc[0]
first_5_rows = df.iloc[:5]

# Select by label
row_by_name = df.loc[df['name'] == 'Alice']
```

The two indexers `.loc` and `.iloc` look similar but mean different things. `.loc` selects by label (the index value or a boolean mask), `.iloc` selects by integer position. When you reset an index after filtering, integer positions stay sequential but labels can have gaps; mixing them up is a frequent source of confusing bugs.

For boolean filtering with multiple conditions, parentheses are required around each condition. `df[df['a'] > 0 & df['b'] > 0]` is a syntax error trap because `&` binds tighter than `>`. Write `df[(df['a'] > 0) & (df['b'] > 0)]` instead.

## Modifying Data

```python
# Add a new column
df['years_employed'] = df['age'] - 22

# Rename columns
df.rename(columns={'old_name': 'new_name'}, inplace=True)

# Replace values
df['status'] = df['status'].replace('active', 'employed')

# Remove duplicates
df = df.drop_duplicates()

# Sort by column
df_sorted = df.sort_values('salary', ascending=False)

# Drop columns
df = df.drop(columns=['unwanted_col'])
```

Notebook hygiene tip: every modification cell should produce output you can verify. After `drop_duplicates`, print `len(df)` to confirm the new size. After `rename`, print `df.columns`. Silent mutations are how notebook bugs survive into the SLURM job that fails three hours into a long run.

## Working with Sagehen Data

::::::::::::::::::::::::::::::::::::: callout

## A typical analysis workflow on Sagehen

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# Load data from /bigdata (lab shared storage)
df = pd.read_csv('/bigdata/lab/<labname>/experiments_2024.csv')

# Explore
print(f"Shape: {df.shape}")
print(df.info())
print(df.describe())

# Analyze
results = df.groupby('condition')['response'].agg(['mean', 'std'])
print(results)

# Visualize
plt.figure(figsize=(10, 6))
results['mean'].plot(kind='bar', yerr=results['std'])
plt.title('Response by Condition')
plt.xlabel('Condition')
plt.ylabel('Mean Response')
plt.tight_layout()
plt.show()

# Save results back to lab storage (NOT /scratch, which gets cleaned)
results.to_csv('/bigdata/lab/<labname>/results/condition_summary.csv')
print("Analysis complete!")
```

::::::::::::::::::::::::::::::::::::::::::::::

Three small details in that workflow are worth pulling out. Source data lives in `/bigdata/lab/<labname>/`, which is your lab's persistent 1 TB allocation. Final results go back to `/bigdata`, not `/scratch`, because `/scratch` is wiped without backups. Plots are produced inline in the notebook so reviewers can re-run cell by cell and reproduce them.

## Jupyter Display Options

Notebooks have rich display capabilities beyond simple print output:

```python
from IPython.display import HTML, Markdown, Image

# Display HTML
HTML("<h1>Hello</h1>")

# Display markdown
Markdown("# Heading\n\nSome text")

# Display images
Image(url='https://example.com/image.png')
```

The most useful of these in practice is `display(df)` for nicely-formatted DataFrames and `Markdown` for inline section headers when you want narrative inside a long analysis notebook. For final analyses you plan to share, `Markdown` cells alongside code make a notebook readable as a written report.

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Data manipulation

Using the weather data from the previous episode (or create it fresh):

```python
import pandas as pd
import numpy as np

np.random.seed(42)
df = pd.DataFrame({
    'date': pd.date_range('2024-01-01', periods=100),
    'temperature': np.random.normal(65, 10, 100),
    'humidity': np.random.normal(60, 15, 100),
    'wind_speed': np.random.exponential(5, 100)
})
```

1. Filter the data to rows where temperature > 70F
2. Calculate statistics (mean, std, min, max) for filtered data
3. Create a new column called 'wind_category' that labels wind speeds as:
   - 'light' if < 5
   - 'moderate' if 5-10
   - 'strong' if > 10
4. Count how many observations fall into each wind category

::::::::::::::: solution

## Solution

```python
# Step 1: Filter to rows where temperature > 70F
warm_days = df[df['temperature'] > 70]
print(f"Number of days with temperature > 70F: {len(warm_days)}")

# Step 2: Calculate statistics for filtered data
print("\nStatistics for warm days (temp > 70F):")
print(f"Mean temperature: {warm_days['temperature'].mean():.2f} F")
print(f"Std deviation: {warm_days['temperature'].std():.2f} F")
print(f"Min: {warm_days['temperature'].min():.2f} F")
print(f"Max: {warm_days['temperature'].max():.2f} F")

# Step 3: Create wind_category column
df['wind_category'] = pd.cut(df['wind_speed'],
                              bins=[0, 5, 10, float('inf')],
                              labels=['light', 'moderate', 'strong'],
                              right=False)

# Step 4: Count observations in each category
print("\nWind speed category counts:")
wind_counts = df['wind_category'].value_counts().sort_index()
print(wind_counts)
```

**Key pandas techniques**:
- `df[df['temperature'] > 70]`: Boolean filtering to select rows meeting a condition
- `.mean(), .std(), .min(), .max()`: Statistical functions on columns
- `pd.cut()`: Binning continuous values into categories
- `.value_counts()`: Counting occurrences of each category

:::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Group-Then-Plot

Using the weather DataFrame from the previous challenge, group by `wind_category` and compute the mean temperature in each category. Make a bar chart of the result with error bars (standard deviation). Save the chart to `/bigdata/lab/<labname>/figures/temp_by_wind.png`.

::::::::::::::: solution

## Solution

```python
import matplotlib.pyplot as plt

stats = df.groupby('wind_category')['temperature'].agg(['mean', 'std'])
print(stats)

plt.figure(figsize=(8, 5))
stats['mean'].plot(kind='bar', yerr=stats['std'], capsize=4)
plt.ylabel('Mean temperature (F)')
plt.title('Temperature by wind category')
plt.tight_layout()
plt.savefig('/bigdata/lab/<labname>/figures/temp_by_wind.png', dpi=150)
plt.show()
```

The `capsize=4` adds visible end caps to error bars. `dpi=150` is enough for a presentation slide; bump to 300 for print-quality figures.

:::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Always inspect shape, dtypes, and null counts as the first cell after loading
- Use `.loc` for label-based selection and `.iloc` for position-based; mixing them is a common bug
- Boolean filters with multiple conditions need parentheses: `df[(a) & (b)]`
- For files over 2 GB, do exploratory work in an interactive SLURM allocation, not on the login node
- Save final results to /bigdata, not /scratch (which is wiped without backups)
- Notebook hygiene: every modification cell should produce verifiable output

::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
