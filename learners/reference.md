---
title: 'Quick Reference'
---

## Keyboard Shortcuts

**Running cells:**

| Action | Shortcut |
|--------|----------|
| Run cell | Ctrl+Enter |
| Run cell and move down | Shift+Enter |
| Run all cells | Menu: Run → Run All Cells |

**Editing:**

| Action | Shortcut |
|--------|----------|
| New cell below | Ctrl+Shift+B |
| New cell above | Ctrl+Shift+A |
| Convert to code | Escape then Y |
| Convert to markdown | Escape then M |
| Delete cell | Select cell, Escape, D, D |
| Undo | Ctrl+Z |
| Save | Ctrl+S |

**Navigation:**

| Action | Shortcut |
|--------|----------|
| Go to line | Ctrl+G |
| Find | Ctrl+F |
| Find and replace | Ctrl+H |

### pandas Quick Reference

**Loading data:**

```python
import pandas as pd
df = pd.read_csv('file.csv')
df = pd.read_excel('file.xlsx')
df = pd.read_json('file.json')
```

**Exploring:**

```python
df.head()              # First 5 rows
df.tail()              # Last 5 rows
df.shape               # (rows, columns)
df.info()              # Data types
df.describe()          # Summary statistics
df['column'].unique()  # Unique values
```

**Selecting:**

```python
df['column']           # One column
df[['col1', 'col2']]   # Multiple columns
df[df['age'] > 25]     # Filter
df.iloc[0]             # First row
df.loc[df['id'] == 5]  # By label
```

**Modifying:**

```python
df['new'] = df['a'] + df['b']        # Add column
df.rename(columns={'old': 'new'})    # Rename
df.drop('col', axis=1)               # Remove column
df.fillna(0)                         # Fill missing
df.groupby('cat').mean()             # Group by
```

### NumPy Quick Reference

**Create arrays:**

```python
import numpy as np
arr = np.array([1, 2, 3])
arr = np.zeros((3, 4))
arr = np.ones((3, 4))
arr = np.linspace(0, 10, 100)
arr = np.random.randn(100)
```

**Operations:**

```python
arr.shape              # Dimensions
arr.mean()             # Average
arr.std()              # Standard deviation
arr.min(), arr.max()   # Min, max
arr * 2                # Multiply
arr[0:5]               # First 5
arr[arr > 5]           # Filter
```

### matplotlib Quick Reference

**Basic plot:**

```python
import matplotlib.pyplot as plt
x = [1, 2, 3, 4]
y = [1, 4, 2, 3]
plt.plot(x, y)
plt.title('Title')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()
```

**Plot types:**

```python
plt.plot(x, y)                    # Line
plt.scatter(x, y)                 # Points
plt.hist(data, bins=30)           # Histogram
plt.bar(categories, values)       # Bar chart
```

**Subplots:**

```python
fig, axes = plt.subplots(2, 2)
axes[0, 0].plot(x, y)
axes[0, 1].scatter(x, y)
plt.show()
```

### IPython Magic Commands

```python
%timeit code                # Time execution
%matplotlib inline          # Show plots inline
%pwd                        # Current directory
%ls                         # List files
%run script.py              # Run file
%whos                       # List variables
%clear                      # Clear output
```

### Sagehen HPC Storage

| Path | Size | Backed Up | Purpose |
|------|------|-----------|---------|
| `/rhome/<myusername>` | 100 GB | Yes | Home directory |
| `/bigdata/lab/<labname>` | 1 TB | Yes | Lab shared storage |
| `/scratch/username` | SSD | No | Fast temporary |

### Common Errors

**NameError: name 'x' is not defined**
- Cause: Variable not created yet
- Fix: Run cell that creates x first

**ModuleNotFoundError: No module named 'numpy'**
- Cause: Package not installed
- Fix: `pip install numpy` in terminal, then restart kernel

**FileNotFoundError: no such file**
- Cause: Wrong file path
- Fix: Use absolute path or verify filename

**Cell hangs**
- Cause: Infinite loop or too much data
- Fix: Click stop button or Kernel → Interrupt

### Conda Commands

```bash
# List environments
conda env list

# Create environment
conda create --name myenv python=3.11 numpy pandas

# Activate
conda activate myenv

# Install packages
conda install numpy
pip install package

# Export for sharing
conda env export > environment.yml

# Create from export
conda env create -f environment.yml
```

### Converting Notebooks

**To Python script:**
```bash
jupyter nbconvert --to script notebook.ipynb
```

**To HTML:**
```bash
jupyter nbconvert --to html notebook.ipynb
```

**To PDF:**
```bash
jupyter nbconvert --to pdf notebook.ipynb
```

### Reproducibility Checklist

- [ ] environment.yml updated (conda env export > environment.yml)
- [ ] Notebook runs start-to-finish without errors
- [ ] Kernel → Restart, then Run → Run All Cells succeeds
- [ ] Cell outputs are visible
- [ ] Documentation is clear (markdown cells)
- [ ] Data paths work for others
- [ ] Results are saved

### Resources

- **Jupyter docs**: https://jupyter.org/documentation
- **pandas docs**: https://pandas.pydata.org/
- **matplotlib docs**: https://matplotlib.org/
- **OnDemand**: https://ondemand.hpc.pomona.edu/
- **Sagehen info**: https://pomona-college.github.io/

### Getting Help

- **Email**: its-hpc@pomona.edu
- **Slack**: #hpc-help (Pomona CS Slack)
- **Stack Overflow**: https://stackoverflow.com/ (search your error)
- **Jupyter Issues**: https://github.com/jupyter/notebook/issues

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
