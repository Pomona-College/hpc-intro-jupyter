---
title: 'Python Fundamentals in Notebooks'
teaching: 20
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I write Python code in notebooks?
- How do I import and use common data science libraries?
- How do I load data from CSV and other formats?
- What's special about IPython magic commands?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Write and execute Python code in notebook cells
- Import and use NumPy, pandas, and matplotlib
- Load data from CSV and other file formats
- Use IPython magic commands for enhanced functionality

::::::::::::::::::::::::::::::::::::::::::::::

## Python in Jupyter

Jupyter notebooks run Python code almost identically to regular Python scripts, but with some enhancements. Let's explore the main differences and capabilities.

### Basic Python syntax

Standard Python works as expected:

```python
# Variables and types
name = "Alice"
age = 30
scores = [85, 92, 78, 95]
data_dict = {"name": "Bob", "age": 25}

# Loops and conditionals
for score in scores:
    if score >= 90:
        print(f"{score} is excellent!")

# Functions
def calculate_average(values):
    return sum(values) / len(values)

avg = calculate_average(scores)
print(f"Average: {avg:.2f}")
```

This all works in Jupyter exactly as it would in a script.

## Importing Libraries

Most data science work relies on libraries. Common ones:

### NumPy (numerical computing)

```python
import numpy as np

# Create arrays
arr = np.array([1, 2, 3, 4, 5])
matrix = np.ones((3, 4))

# Array operations
result = arr * 2
print(result)  # [2 4 6 8 10]

# Statistics
mean = np.mean(arr)
std = np.std(arr)
```

### pandas (data manipulation)

```python
import pandas as pd

# Create a DataFrame (like an Excel table)
data = {
    'name': ['Alice', 'Bob', 'Carol'],
    'age': [30, 25, 28],
    'salary': [50000, 45000, 55000]
}
df = pd.DataFrame(data)

# Access columns
print(df['name'])

# Statistics
print(df.describe())

# Filter rows
high_earners = df[df['salary'] > 50000]
```

### matplotlib (visualization)

```python
import matplotlib.pyplot as plt

# Create a line plot
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 5, 8]
plt.plot(x, y)
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.title('Simple Plot')
plt.show()  # Important! Displays the plot
```

## Loading Data from Files

A typical workflow: Load data from CSV (or other formats) and explore it.

### From CSV files

```python
import pandas as pd

# Load CSV file (use full path for clarity)
df = pd.read_csv('/rhome/<myusername>/data/experiments.csv')

# See first few rows
print(df.head())

# Get information about the DataFrame
print(df.info())

# Summary statistics
print(df.describe())

# Check shape (rows, columns)
print(f"Data has {df.shape[0]} rows and {df.shape[1]} columns")
```

### From other formats

pandas supports many formats:

```python
# Excel file
df = pd.read_excel('data.xlsx')

# JSON
df = pd.read_json('data.json')

# HDF5 (efficient for large datasets)
df = pd.read_hdf('data.h5', key='dataset')

# Pickle (Python-specific, fast)
df = pd.read_pickle('data.pkl')
```

## IPython Magic Commands

Jupyter uses **IPython** (Interactive Python), which includes special commands called "magic" commands. These start with `%` (line magic) or `%%` (cell magic).

::::::::::::::::::::::::::::::::::::: callout

### Commonly used magic commands

**Timing code:**
```python
%timeit sum(range(1000000))    # Time a single line
%time x = sum(range(1000000))  # Time once (not averaged)
```

**Displaying output:**
```python
%matplotlib inline             # Show plots inline (usually default)
%whos                          # List all variables in memory
```

**Running external files:**
```python
%run my_script.py              # Run a Python script
%load my_code.py               # Load code from file into a cell
```

::::::::::::::::::::::::::::::::::::::::::::::

## Output Handling

By default, Jupyter only displays the last output in a cell. To display multiple outputs:

```python
# Method 1: Use print()
print("First output")
print("Second output")

# Method 2: Use display()
from IPython.display import display
display("First output")
display("Second output")

# Method 3: Semicolon suppresses output
x = 5
y = 10
z = x + y;  # Semicolon suppresses output
```

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Load and explore data

1. Create a new notebook cell and load some sample data:
   ```python
   import pandas as pd
   import numpy as np

   # Create sample dataset
   np.random.seed(42)
   df = pd.DataFrame({
       'date': pd.date_range('2024-01-01', periods=100),
       'temperature': np.random.normal(65, 10, 100),
       'humidity': np.random.normal(60, 15, 100),
       'wind_speed': np.random.exponential(5, 100)
   })
   ```

2. In subsequent cells, explore the data:
   - Print `df.head()` to see first rows
   - Print `df.info()` to see data types
   - Print `df.describe()` for statistics
   - Calculate mean temperature and humidity

Document each step with markdown cells explaining what you're doing.

::::::::::::::: solution

## Solution

**Cell 1 (Markdown):**
```markdown
# Weather Data Analysis

Exploring a simulated dataset of 100 days of weather measurements.
```

**Cell 2 (Code):** Create the dataset (code above).

**Cell 3 (Code):**
```python
print("First 5 rows of the dataset:")
print(df.head())
```

**Cell 4 (Code):**
```python
print("\nDataFrame Information:")
df.info()
```

**Cell 5 (Code):**
```python
mean_temp = df['temperature'].mean()
mean_humidity = df['humidity'].mean()
print(f"Mean temperature: {mean_temp:.2f} F")
print(f"Mean humidity: {mean_humidity:.2f}%")
```

Expected output includes a nicely formatted table with dates, temperatures (around 65F), humidity (around 60%), and wind speeds, followed by calculated means.

:::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Python code runs normally in Jupyter cells, with enhanced display capabilities
- NumPy, pandas, and matplotlib are the core data science libraries
- pandas can load data from CSV, Excel, JSON, HDF5, and many other formats
- Magic commands (% and %%) add special IPython functionality like timing code
- Use print() or display() to show multiple outputs from a single cell

::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
