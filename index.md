---
title: 'Introduction to Jupyter Notebooks on Sagehen'
subtitle: 'Interactive Python development on the Pomona College HPC cluster'
---

## Welcome!

This workshop teaches you how to use **Jupyter Notebooks** for interactive Python development on the **Sagehen HPC cluster**. Jupyter Notebooks combine executable code, text explanations, and visualizations in a single document, making them ideal for exploratory analysis, teaching, and scientific computing.

## Why take this workshop?

Jupyter Notebooks are powerful tools for computational research, and when combined with the resources of an HPC cluster, they become even more valuable. After this workshop, you will be able to:

- Understand what Jupyter Notebooks are and why they're useful for research
- Launch Jupyter on Sagehen using the OnDemand portal
- Work with different cell types (code, markdown) and understand the notebook execution model
- Write Python code that explores data and produces visualizations
- Manage Python environments and install packages for your notebooks
- Apply best practices for reproducible and shareable notebooks
- Convert notebooks to different formats and automate analyses

:::::::::::::::::::::::::::::::::::::::: prereq

## What you'll need

- **Your Pomona College account** with HPC access
- **A web browser** (Chrome, Firefox, Safari, or Edge)
- **Access to the Sagehen cluster** (sagehen.hpc.pomona.edu)
- **Basic Python knowledge** (variables, functions, simple data structures)
- **30-40 minutes** for the full workshop

If you're new to Python, we recommend learning Python basics first. This workshop assumes you can write simple Python statements.

::::::::::::::::::::::::::::::::::::::::::::::

## Workshop structure

This workshop is organized as follows:

| Episode | Time | Topic |
|---------|------|-------|
| 1  | 15 min + 5 ex  | What Are Jupyter Notebooks? — history, use cases, and why notebooks on HPC |
| 2  | 15 min + 10 ex | Launching Jupyter on Sagehen via the OnDemand portal with proper resource requests |
| 3  | 15 min + 10 ex | Notebook interface basics — JupyterLab layout, file browser, and the kernel model |
| 4  | 20 min + 15 ex | Working with cells — code vs. markdown, execution order, and editing shortcuts |
| 5  | 20 min + 10 ex | Python fundamentals in notebooks — imports, variables, control flow |
| 6  | 25 min + 20 ex | Data analysis in notebooks — loading, exploring, and summarising data |
| 7  | 15 min + 10 ex | Visualization in notebooks — matplotlib basics and inline figures |
| 8  | 20 min + 15 ex | Managing kernels and environments — conda envs and custom kernels for Jupyter |
| 9  | 15 min + 10 ex | Sharing and exporting — HTML, PDF, .py, and integrating with version control |
| 10 | 15 min + 10 ex | Best practices for reproducible, shareable notebooks |

**Total teaching time: ~5 hours** (175 minutes teaching + 115 minutes exercises, plus breaks)

## Key technologies

This workshop focuses on tools available on Sagehen:

- **JupyterLab** - Interactive notebook environment (modern Jupyter interface)
- **Python 3** - Programming language (via conda)
- **conda** - Environment and package management
- **Sagehen HPC cluster** - Computing resources with module system
- **OnDemand portal** - Web interface for cluster access (https://ondemand.hpc.pomona.edu/)

## Learning outcomes

By the end of this workshop, you will be able to:

- Explain what Jupyter Notebooks are and their advantages for computational research
- Launch JupyterLab on Sagehen with appropriate resource requests
- Create and execute notebook cells with proper output handling
- Write Python code that loads, processes, and visualizes data
- Create and switch between Python environments
- Manage dependencies reproducibly using environment files
- Export notebooks to HTML, PDF, or Python scripts
- Apply version control best practices to notebook-based workflows

::::::::::::::::::::::::::::::::::::: callout

## Getting help

If you encounter issues during the workshop:
- **Email**: its-hpc@pomona.edu (most reliable)
- **Slack**: #hpc-help channel (Pomona CS Slack workspace)
- **Office hours**: See ITS-HPC website for Andrew Wilson's availability
- **Troubleshooting**: Check the [Reference](learners/reference.md) section for common issues

::::::::::::::::::::::::::::::::::::::::::::::::


## Before you begin

Please complete the following before the workshop:

1. **Verify HPC access**: Try logging into https://ondemand.hpc.pomona.edu/ - if it works, you're ready
2. **Check browser compatibility**: We support modern Chrome, Firefox, Safari, and Edge
3. **Test internet connection**: Jupyter requires a persistent network connection
4. **Optional: Create a work directory**: `ssh sagehen && mkdir -p ~/jupyter-workshop`

Ready to get started? Let's dive in!

---

**Questions or suggestions?** Please contact its-hpc@pomona.edu or open an issue on our [GitHub repository](https://github.com/Pomona-College/hpc-intro-jupyter).

