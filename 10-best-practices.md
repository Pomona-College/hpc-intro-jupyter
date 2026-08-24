---
title: 'Best Practices'
teaching: 15
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I organize notebooks for reproducibility?
- What are best practices for naming and documenting?
- How do I scale notebooks to production workflows?
- What common mistakes should I avoid?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Apply organizational best practices to notebooks
- Document notebooks for clarity and reproducibility
- Understand when to convert notebooks to batch jobs
- Avoid common notebook pitfalls

::::::::::::::::::::::::::::::::::::::::::::::

## Organizing Notebooks for Reproducibility

### Directory structure

Organize your project to separate code, data, and results:

```
my_analysis/
  README.md                    # Project overview
  environment.yml              # Conda environment (always include!)
  notebooks/
    01_data_loading.ipynb      # Load and explore data
    02_analysis.ipynb          # Main analysis
    03_visualization.ipynb     # Create figures
  data/
    raw/                       # Original, never modified
      experiment.csv
    processed/                 # Cleaned versions
      experiment_clean.csv
  scripts/
    functions.py               # Reusable code
  results/
    figures/
      plot.png
    tables/
      summary.csv
  ANALYSIS_LOG.md              # What you did and why
```

### File naming conventions

```
# Good: Descriptive and sequential
01_data_loading.ipynb
02_exploratory_analysis.ipynb
03_statistical_tests.ipynb

# Avoid: Vague names
analysis.ipynb
notebook.ipynb
draft_v3_final_REAL.ipynb
```

### Documentation practices

At the top of each notebook, include a markdown cell:

```markdown
# Analysis of Temperature Trends

**Purpose**: Analyze temperature patterns from Sagehen weather station
**Date**: 2024-03-06
**Author**: Alice Johnson
**Data**: /bigdata/lab/<labname>/weather/sagehen_2024.csv
**Output**: Results saved to /rhome/alice/results/

## Methods

1. Load temperature data for Jan-Feb 2024
2. Calculate daily averages
3. Perform trend analysis with linear regression
4. Create visualization

## Dependencies

See environment.yml for all package versions.
```

## Scaling Notebooks to Batch Jobs

When your notebook works well, you may want to scale it:

### Interactive notebook (for development)

```python
# In notebook
df = pd.read_csv('data.csv')
results = analyze(df)
plot_results(results)
```

### Batch script (for production)

Convert to Python script and run on cluster:

```bash
#!/bin/bash
#SBATCH --job-name=analysis
#SBATCH --time=4:00:00
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G
#SBATCH --partition=amd

module load miniconda3
conda activate analysis

python analysis.py
```

Then submit with `sbatch analysis.sbatch`.

::::::::::::::::::::::::::::::::::::: callout

### Best of both worlds

1. Develop analysis in Jupyter (interactive, exploratory)
2. Convert to script when approach is solid
3. Submit script as batch job (automated, scalable)
4. Use Jupyter again to analyze batch results

::::::::::::::::::::::::::::::::::::::::::::::

## Avoiding Common Mistakes

**Mistake 1: Kernel state dependencies.** If you define `x = 5` in one cell and use `x` 20 cells later, that value might have changed. Keep related code together or clearly document dependencies between cells.

**Mistake 2: Relative paths that break.** Using `pd.read_csv('data.csv')` works for you but fails for collaborators. Use absolute paths like `/rhome/<myusername>/project/data/data.csv` or paths relative to the project root.

**Mistake 3: Outdated package versions.** Your notebook runs today but breaks next month when packages update. Always export `conda env export > environment.yml` and include it with your project.

**Mistake 4: Long-running cells without checkpoints.** If a cell processes a million records and fails halfway through, you lose all progress. Break large operations into chunks and save intermediate results to disk.

::::::::::::::::::::::::::::::::::::: callout

## Sharing notebooks ethically

Before sharing, consider:
- **Data privacy**: Remove or anonymize sensitive data
- **Credentials**: Never include passwords or API keys
- **Licensing**: Include license file (CC-BY-4.0 is good for research)
- **Acknowledgments**: Credit data sources and collaborators
- **Reproducibility**: Verify everything works before sharing

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

## Reproducible analysis checklist

Before sharing or publishing your work:
- [ ] **Environment documented**: `environment.yml` file included
- [ ] **Data accessible**: Clear instructions for accessing data
- [ ] **Code runs top-to-bottom**: Kernel restart then Run All Cells succeeds
- [ ] **Outputs explained**: Markdown cells explain each analysis step
- [ ] **Visualizations labeled**: All plots have titles, axis labels, legends
- [ ] **Parameters clear**: Any magic numbers have explanations
- [ ] **Version controlled**: Repository with history
- [ ] **README included**: Instructions for reproducing analysis

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Create a reproducible project

Create a complete, reproducible analysis project:
1. Create a directory structure:
   ```bash
   mkdir -p my_analysis/notebooks my_analysis/data/raw my_analysis/data/processed my_analysis/results/figures my_analysis/results/tables
   ```
2. Create environment.yml:
   ```bash
   conda env export > my_analysis/environment.yml
   ```
3. Initialize Git:
   ```bash
   cd my_analysis
   git init
   echo "data/raw/*" > .gitignore
   git add .
   git commit -m "Initial project structure"
   ```
4. Create a notebook in notebooks/ that loads a sample dataset and creates a visualization

::::::::::::::: solution

## Solution

After completing the steps, your project looks like:
```
my_analysis/
  environment.yml
  .gitignore
  notebooks/
    01_analysis.ipynb
  data/
    raw/
    processed/
  results/
    figures/
    tables/
```

**Why this structure is reproducible:**
- `environment.yml` ensures exact package versions
- Directory organization is clear and standard
- `.gitignore` prevents committing huge data files
- README documents how to set up and run everything

:::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Test reproducibility

Ensure your notebook is truly reproducible:
1. Open your notebook in JupyterLab
2. Kernel then Restart Kernel
3. Run then Run All Cells
4. Fix any errors that appear
5. Once it runs perfectly, do steps 2-4 again to double-check

Save the notebook. It's now verified to work from a clean state. This is the standard before sharing!

::::::::::::::: solution

## Solution

**Step 1-2: Restart kernel** clears all variables (simulates someone running your notebook for the first time).

**Step 3: Run all cells** executes every cell from top to bottom. Each cell number should increase sequentially: [1], [2], [3], etc.

**Step 4: Check for errors.** Common issues:
- `NameError: name 'x' is not defined`: Variable used before being defined
- `FileNotFoundError`: Data file path is wrong
- `ModuleNotFoundError`: Package not installed in your environment

**Why this matters**: You've proven it works from a clean state. Someone else can run your notebook and get the same results. This is the difference between "works for me" and truly reproducible research.

:::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Organize projects with clear directory structure and naming conventions
- Document each notebook with purpose, author, data sources, and methods
- Scale from Jupyter to batch jobs: develop interactively, then convert to scripts
- Avoid common mistakes: kernel state issues, relative paths, outdated packages
- Always export environment.yml for reproducibility
- Test reproducibility: Restart kernel and run all cells before sharing

::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
