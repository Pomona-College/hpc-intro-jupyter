---
title: 'What Are Jupyter Notebooks?'
teaching: 15
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- What is a Jupyter Notebook?
- Why are Jupyter Notebooks useful for computational research?
- How do Jupyter Notebooks differ from regular Python scripts?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand what Jupyter Notebooks are and their key features
- Recognize use cases where Jupyter Notebooks are ideal
- Understand the difference between notebooks and scripts
- Identify when to use notebooks vs. other tools

::::::::::::::::::::::::::::::::::::::::::::::

## What is a Jupyter Notebook?

**Jupyter Notebook** is an open-source web application that allows you to create and share documents containing:

- **Live code**: Executable Python, R, Julia, and 40+ other languages
- **Output**: Formatted results, plots, images, tables
- **Narrative text**: Written explanation in Markdown, including equations
- **Visualizations**: Plots, charts, and interactive graphics

All of these elements live in a single document, in your web browser, making it easy to explore data, test ideas, and communicate your work.

::::::::::::::::::::::::::::::::::::: callout

## Where does the name come from?

Jupyter evolved from **IPython** (Interactive Python), created in 2001 by Fernando Pérez. In 2014, the IPython team created Jupyter Notebooks, extending the interactive concept to include rich output and the notebook format we know today.

The name "Jupyter" comes from the three core languages it originally supported: **Ju**lia, **Pyt**hon, and **R**.

Today, Jupyter supports over 100 languages through different "kernels" (the execution engines that run code), but Python remains the most common.

::::::::::::::::::::::::::::::::::::::::::::::

## Anatomy of a Jupyter Notebook

A Notebook is organized into **cells**, where each cell contains either:

### Code cells

```python
import numpy as np
import matplotlib.pyplot as plt

# Create data
x = np.linspace(0, 10, 100)
y = np.sin(x)

# Create plot
plt.plot(x, y)
plt.title('Sine Wave')
plt.xlabel('x')
plt.ylabel('sin(x)')
plt.show()
```

When you run a code cell, the code executes on the kernel (the Python interpreter) and results appear below the cell.

### Markdown cells

These contain formatted text, written in **Markdown** (a simple markup language):

```markdown
# Analysis of Temperature Data

This notebook analyzes temperature measurements from the Sagehen weather station.

## Methods

We collected data every hour from January to March 2024.

## Results

- Mean temperature: 45F
- Maximum: 82F
- Minimum: 18F
```

When you run a markdown cell, it displays as formatted text. This lets you combine explanation with code in a single document.

### Raw cells (less common)

Raw cells contain unformatted text, useful for specific export formats. Most notebooks use code and markdown cells.

## Why Jupyter Notebooks?

### Advantages for research

**Interactive exploration**: Rather than writing a complete script, then running it, then debugging, Jupyter lets you develop code interactively. Run one cell, see results, then modify and run again. This tight feedback loop accelerates discovery.

**Reproducible analysis**: Your code, results, and explanations live together in one document. This makes it much easier for collaborators to understand what you did and reproduce your work.

**Rich output**: Plots appear inline below your code. Tables are formatted nicely. Equations can be written in LaTeX. This produces publication-quality results without leaving the notebook.

**Easy to learn**: Jupyter's interface is intuitive. You don't need to know Git, command-line tools, or complex IDEs to get started. For students and researchers new to computing, Jupyter is an excellent entry point.

**Shareable**: You can save notebooks as `.ipynb` files and email them to collaborators. They can open the same notebook and see your code, output, and explanations. (The `.ipynb` format is JSON-based text, so it works with version control.)

**Multiple languages**: While we focus on Python in this workshop, Jupyter supports R, Julia, and many others. One user can work in their preferred language in a single environment.

## When to use Jupyter vs. other tools

**Use Jupyter Notebooks for:**
- Exploratory analysis (understanding new data)
- Interactive visualization and data exploration
- Teaching and learning (great for tutorials)
- Communicating results to non-technical audiences
- Data science and statistical analysis workflows
- Prototyping analysis pipelines before scaling with SLURM

**Use regular Python scripts for:**
- Long-running analyses (better for batch jobs via SLURM)
- Production pipelines that run unattended
- Code that needs to be imported into other programs
- Performance-critical code where every millisecond counts
- Large analyses that generate thousands of files

**Use Jupyter + SLURM together for:**
- Developing and testing code interactively in Jupyter
- When satisfied with the approach, convert to a script
- Submit the script as a batch job to SLURM for production
- Use Jupyter again to analyze the results

::::::::::::::::::::::::::::::::::::: discussion

## Choosing the right tool

Ask yourself these questions:
- **Do I need to explore and understand data interactively?** Use Jupyter
- **Will this run for hours unattended?** Use a script + SLURM batch job
- **Do I need to explain my work to non-programmers?** Use a Jupyter notebook
- **Am I just testing an idea quickly?** Start in Jupyter, convert to script if needed
- **Do I need publication-quality visualizations?** Jupyter is great for this

The best practice: **Start with Jupyter for exploration, then convert to scripts for production work.**

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Jupyter Notebook use case evaluation

For each scenario, decide: Is Jupyter Notebook ideal, useful but not perfect, or not recommended?
1. **Scenario A**: Training a deep neural network on 100 million images that will take 48 hours
2. **Scenario B**: Exploring a new dataset, creating visualizations, and testing analysis ideas
3. **Scenario C**: Documenting your lab's data analysis pipeline for new students
4. **Scenario D**: Writing production code that multiple applications depend on

For each, write 1-2 sentences explaining your reasoning.

::::::::::::::: solution

## Solution

**Scenario A**: **Not recommended**. Long-running training jobs are better suited for batch scripts submitted to SLURM (e.g., sbatch). Jupyter notebooks require active browser connections and aren't designed for unattended 48-hour jobs. Use a Python script with SLURM instead, and use Jupyter afterward to analyze results.

**Scenario B**: **Ideal**. This is exactly what Jupyter is designed for. Interactive exploration, immediate feedback, and inline visualizations make it perfect for understanding new data and testing different analysis approaches before committing to a final approach.

**Scenario C**: **Ideal**. Jupyter notebooks are excellent for documentation and teaching. A notebook with markdown explanations, working code examples, and output demonstrates the pipeline step-by-step, making it easy for students to learn and adapt the process for their own data.

**Scenario D**: **Not recommended**. Production code that other applications depend on should be modular Python files (modules) or packages. Notebooks are harder to import and test, and their state-based execution makes them risky for critical workflows. Convert to .py scripts and use proper software engineering practices.

:::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Jupyter Notebooks combine code, output, and narrative text in interactive documents
- They're ideal for exploration, teaching, and communicating research
- Notebooks are great for development but scripts are better for long-running production jobs
- The best practice: Start with Jupyter, convert to scripts when ready to scale

::::::::::::::::::::::::::::::::::::::::::::::
