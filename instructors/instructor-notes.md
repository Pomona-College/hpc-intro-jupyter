---
title: 'Instructor Notes'
---

## Workshop Overview

This workshop introduces Jupyter Notebooks for interactive Python development on the Sagehen HPC cluster. Total time: ~3 hours including breaks and challenges.

**Target audience:** Pomona College researchers and students using HPC for data analysis or scientific computing

**Prerequisites:**
- Pomona HPC account (active access to Sagehen cluster)
- Basic Python knowledge (variables, functions, loops)
- Access to web browser and internet
- DUO authentication set up

## Learning Outcomes

After this workshop, learners can:

1. Understand what Jupyter Notebooks are and why they're useful for research
2. Launch JupyterLab on Sagehen using the OnDemand portal
3. Create and manage cells (code and markdown)
4. Write Python code to load, explore, and visualize data
5. Create and manage Python environments with conda
6. Apply best practices for reproducible notebooks
7. Convert notebooks to scripts, HTML, and PDF

## Episode-by-Episode Guide

### Episode 1: Introduction to Jupyter Notebooks (45 min total)

**Teaching: 30 min | Exercises: 10 min**

**Main message:** Jupyter Notebooks combine code, output, and narrative in interactive documents, making them powerful for exploration and communication.

**Key points to emphasize:**
- Notebooks are interactive (write code, run, see results immediately)
- Different from regular Python scripts (scripts run all-at-once; notebooks are cell-by-cell)
- Useful for research because they blend explanation with results
- On HPC, Jupyter lets you use powerful computing resources interactively

**Live demonstration ideas:**
- Show a Jupyter notebook running on your screen (via projector)
- Demonstrate code cell + output (e.g., plotting)
- Demonstrate markdown cell (formatted text with equations)
- Show how to run individual cells, not just scripts

**Common misconceptions to address:**
- "It's just a text editor" → No, it's an interactive IDE-like environment
- "Notebooks are for beginners" → Actually useful for professionals too
- "I have to run the whole notebook every time" → No, run individual cells as needed
- "Notebooks aren't reproducible" → They can be, with proper practices (covered later)

**If learners ask about:**
- **Production use**: "We cover batch jobs in Episode 6; Jupyter is for development/exploration"
- **Comparison to RStudio**: "Similar concept; Jupyter works for Python and 100+ languages"
- **Cloud notebooks (Google Colab, etc.)**: "Sagehen Jupyter gives you local HPC resources directly"

**Challenge notes:**
- Challenge 1.1: Reflection helps learners connect to their own work
- Challenge 1.2: Thinking through scenarios cements use-case understanding
- Give 5 min for each, let people discuss with neighbors

### Episode 2: Launching Jupyter on Sagehen (45 min total)

**Teaching: 25 min | Exercises: 20 min**

**Main message:** OnDemand is a simple web interface for launching Jupyter; understanding resource requests is key.

**Key points:**
- OnDemand is a web portal (https://ondemand.hpc.pomona.edu/)
- No command-line knowledge needed
- DUO authentication required (same MFA as Pomona login)
- Resource requests (CPU, RAM, time) matter: asking for too much means long waits

**Live demo:**
1. Show OnDemand login page
2. Walk through logging in
3. Navigate to Interactive Apps
4. Show JupyterLab launch form and explain each field
5. Submit a job request
6. Show "waiting for server to start" page
7. Show JupyterLab interface once it starts
8. Open a sample notebook

**Common issues and solutions:**

| Issue | Cause | Solution |
|-------|-------|----------|
| Can't log into OnDemand | Wrong credentials or no account | Verify HPC account status; contact its-hpc@pomona.edu |
| DUO prompt doesn't appear | Browser issue or disabled setting | Try incognito mode; clear cache; try different browser |
| Server takes >5 min to start | Cluster busy or too many resources requested | Wait longer; try with fewer cores/RAM; try later |
| Can't see JupyterLab | JavaScript disabled or old browser | Enable JavaScript; try modern browser (Chrome, Firefox) |
| "Permission denied" accessing /bigdata | Not in lab group | Contact its-hpc@pomona.edu; only lab members can access |

**Teaching tips:**
- Do the launch live (not just screenshots)
- Let learners do it simultaneously at their laptops
- Circulate and help those with login issues
- If cluster is down, use pre-recorded video or screenshots
- Have a backup Jupyter instance already running to demo

**Challenge notes:**
- Challenge 2.1 (Launch JupyterLab): This is hands-on; expect 5-10 min for everyone to get running
  - Help those having login issues while others continue
  - Don't move on until everyone has a running JupyterLab
  - This is a critical milestone!
- Challenge 2.2 (Explore file system): Learners practice file navigation (5 min)
- Challenge 2.3 (Access data): Verify cluster storage is accessible (5 min)

**Success criterion:** Everyone has a JupyterLab window open and can see their home directory.

### Episode 3: Notebook Basics (55 min total)

**Teaching: 35 min | Exercises: 20 min**

**Main message:** Notebooks are sequences of cells; understanding execution order and cell types is essential.

**Key points:**
- Two main cell types: code and markdown
- Cells execute in the order you run them (not necessarily top-to-bottom)
- The kernel maintains state across cells
- Markdown cells are for documentation (using markdown syntax)

**Live demo:**
1. Create a new notebook (in running JupyterLab)
2. Create a code cell: `x = 5`
3. Run it (Ctrl+Enter); show [1] notation
4. Create markdown cell; write formatted text
5. Run markdown cell; show it formats nicely
6. Create another code cell: `print(x + 10)` and run it
7. Demonstrate: restart kernel → run cell 3 → error (because x undefined)
8. Demonstrate: run cells in order → success
9. Show multiple terminal windows (useful feature)

**Common misconceptions:**
- "Cells always run top-to-bottom" → No! They run in order you execute them
- "Markdown is just comments" → No! It's formatted text (bold, italics, equations, etc.)
- "Variables are local to cells" → No! They're global in the kernel
- "Restarting kernel deletes files" → No! Only clears variables; files stay on disk

**Timing note:** Episode 3 has substantial content (cells, execution, markdown, kernel). May take longer than 35 min teaching. Be prepared to extend by 10 min if needed.

**Challenge notes:**
- Challenge 3.1 (Multi-cell notebook): Learners create a notebook with imports, markdown, plots
  - Takes 10 min; check that plots appear
- Challenge 3.2 (Execution order): Demonstrates the pitfalls of out-of-order execution
  - Key conceptual challenge; make sure learners understand WHY it failed
  - Have them explain execution order back to you
- Challenge 3.3 (Markdown): Practice formatting
  - Show them the difference between raw markdown and rendered output
  - Keep it short (5 min)

**Success criterion:** Learners understand: cells run in order executed, kernel state persists, restart clears state.

### Episode 4: Python in Notebooks (65 min total)

**Teaching: 40 min | Exercises: 25 min**

**Main message:** Jupyter excels at interactive data exploration; pandas + matplotlib make it powerful.

**Key points:**
- Standard Python works in notebooks
- pandas is the standard for data manipulation
- matplotlib produces inline plots
- Notebooks are ideal for exploratory analysis

**Live demo:**
1. Load a CSV file with pandas
2. Explore with `.head()`, `.info()`, `.describe()`
3. Filter data: `df[df['age'] > 25]`
4. Create a plot with matplotlib
5. Show plot appears inline
6. Modify plot (add title, labels); show live iteration

**Emphasize:**
- This is how real data analysis looks
- Iterative: try something, see result, modify, repeat
- Much faster than: script → run → check output → edit script → run again
- Jupyter is ideal for this workflow

**Teaching tips:**
- Use real-world or relatable data (temperature, survey results, sports stats)
- Show mistakes and fix them (debugging in real-time is educational)
- Point out how inline plots make it easy to see if analysis is working
- Magic commands (% commands) are optional; mention but don't over-explain

**Challenge notes:**
- Challenge 4.1 (Load and explore data): 10-15 min
  - Provide sample data CSV or code to generate it
  - Make sure everyone can load and explore
  - Have them calculate at least one statistic
- Challenge 4.2 (Visualize): 10-15 min
  - Line plot, scatter plot, histogram, subplot
  - Some learners may struggle with matplotlib syntax
  - Reference the examples from the episode
- Challenge 4.3 (Manipulate): 10-15 min
  - Filtering, new columns, groupby, categorization
  - More pandas-heavy; some may finish early, others struggle
  - Have advanced exercises ready for fast finishers

**Success criterion:** Learners can load CSV, explore with pandas, create plots with matplotlib.

### Episode 5: Managing Environments (50 min total)

**Teaching: 30 min | Exercises: 20 min**

**Main message:** Python environments isolate packages; conda is the tool; environment files ensure reproducibility.

**Key points:**
- Environments prevent version conflicts
- conda creates and manages environments
- Install kernels to use environments in Jupyter
- environment.yml file enables reproducible sharing

**Live demo (in terminal, not Jupyter):**
1. Load conda: `module load miniconda3`
2. List environments: `conda env list`
3. Create environment: `conda create --name demo python=3.11 numpy pandas`
4. Activate: `conda activate demo`
5. Install kernel: `python -m ipykernel install --user --name demo`
6. Export: `conda env export > environment.yml`
7. Show the YAML file (brief, explain structure)

**Important:** This is command-line work (terminal), not Jupyter.

**Teaching tips:**
- Have learners follow along in a terminal window
- Explain why environments matter with concrete examples
- Keep kernel installation simple (just do it; explain later)
- Don't get bogged down in conda advanced features
- Emphasize: "environment.yml is like saving your setup so others can reproduce it"

**Common issues:**
- Can't find conda → Need to load miniconda3 module
- conda doesn't find a package → Try pip; or check name spelling
- Kernel doesn't appear in Jupyter → Restart Jupyter; verify installation worked
- Permission issues → Usually resolved by activating correct environment

**Challenge notes:**
- Challenge 5.1 (Create environment): 10 min
  - Everyone creates an environment named "workshop"
  - Installs kernel
  - Verify with `conda list`
  - This is hands-on and practical; walk around and help
- Challenge 5.2 (Use in Jupyter): 5-10 min
  - Launch JupyterLab; create notebook with new kernel
  - Verify packages are there
  - Quick confidence booster
- Challenge 5.3 (Export): 5 min
  - `conda env export > file.yml`
  - Look at what's in the file
  - Explain: "This is how you share your environment"

**Success criterion:** Everyone creates an environment, installs a kernel, uses it in Jupyter, exports environment.yml.

### Episode 6: Best Practices (40 min total)

**Teaching: 25 min | Exercises: 15 min**

**Main message:** Organize work, use Git, test reproducibility, share properly.

**Key points:**
- Directory structure separates code, data, results
- Git tracks notebooks; commit clean versions
- Test reproducibility: Restart kernel + Run All
- Convert to scripts or HTML for sharing/production
- Document thoroughly

**Live demo:**
1. Show example project structure (pictures/slides okay)
2. Show notebook → script conversion: `jupyter nbconvert --to script`
3. Show notebook → HTML conversion: `jupyter nbconvert --to html`
4. Demonstrate: Restart kernel → Run All Cells
5. Show environment.yml in project folder

**Discussion points:**
- When to use notebooks (development, exploration, teaching)
- When to convert to scripts (production, batch jobs, long-running)
- Why environment.yml matters (reproducibility, sharing)
- Git best practices (clean commits, meaningful messages)

**Teaching tips:**
- This is more conceptual than practical
- Use slides or diagrams to show project structure
- Emphasize: "These practices save time when collaborating or coming back to old work"
- Some learners may be new to version control; don't assume Git knowledge

**Challenge notes:**
- Challenge 6.1 (Export formats): 10 min
  - Export notebook to script, HTML, PDF
  - Open/view each format
  - Discussion: "When would you use each format?"
  - Good for understanding uses
- Challenge 6.2 (Reproducible project): 10-15 min
  - Create directory structure
  - Create environment.yml
  - Create README
  - Git init and first commit
  - Advanced; some may not finish; that's okay
- Challenge 6.3 (Test reproducibility): 5 min
  - Restart kernel
  - Run all cells
  - Verify no errors
  - Essential habit to build

**Success criterion:** Learners understand reproducibility and best practices; can export notebooks.

## Timing and Pacing

**Total workshop time:** ~3 hours

Recommended timeline:

| Time | Activity | Duration |
|------|----------|----------|
| 0:00-0:10 | Welcome, goals, expectations | 10 min |
| 0:10-0:55 | Episode 1 (Why Jupyter) | 45 min |
| 0:55-1:40 | Episode 2 (Launch Jupyter) | 45 min |
| 1:40-1:50 | Break | 10 min |
| 1:50-2:45 | Episode 3 (Notebook basics) | 55 min |
| 2:45-3:50 | Episode 4 (Python in notebooks) | 65 min |
| 3:50-4:00 | Break | 10 min |
| 4:00-4:50 | Episode 5 (Environments) | 50 min |
| 4:50-5:30 | Episode 6 (Best practices) | 40 min |
| 5:30-5:45 | Q&A, wrap-up | 15 min |

**Total: 5 hours 45 minutes**

**Adjustments:**
- If 3 hours: Do Episodes 1-4 only (skip environments/practices)
- If 4 hours: Do Episodes 1-5 (compress Episode 6)
- If extending: Add more challenges, live demos, or Q&A

## Contingencies

### Cluster is down
- Have a backup: pre-recorded video demo or slides with screenshots
- Discuss concepts without live Jupyter
- Offer to record session for later when cluster is back

### Network issues
- Ensure you have local WiFi or ethernet backup
- Have printed handouts
- Work in smaller groups if bandwidth is limited

### Someone can't access OnDemand
- Have them pair with a neighbor
- Continue workshop while troubleshooting later
- Document issue to improve setup instructions

### Learners have very different experience levels
- Pair advanced learners with beginners
- Have optional advanced challenges ready (they'll finish faster)
- Don't let advanced learners dominate; give everyone air time

### Questions go very deep
- "That's a great question! Let's chat after workshop"
- Keep momentum; don't derail other learners
- Document for future workshops

## Assessment

### Informal assessment (during workshop)
- Observe learners during challenges
- Ask "What did that error mean?" or "Why did we restart the kernel?"
- Check if people are engaged or lost

### Formal assessment (optional)
- Brief quiz at end: 5-10 questions on key concepts
- Have learners demonstrate: launch Jupyter, create notebook, plot data
- Ask: "How would you explain Jupyter to a colleague?"

### Feedback survey (recommended)
Ask at end:
1. What was most useful?
2. What was confusing?
3. Will you use Jupyter for your research? (Yes/No/Maybe)
4. What else would help?
5. Overall, how helpful? (1-5 scale)

This feedback shapes future workshops.

## Teaching Tips

### Building confidence
- Start simple; build complexity gradually
- Celebrate wins: "Great! You just created your first notebook!"
- Normalize errors: "Oh, we got an error! Let's debug together. This is normal."

### Engagement
- Vary teaching styles (demo, live coding, hands-on practice)
- Tell stories: "In my research, I used Jupyter for..."
- Ask questions: "What do you think will happen if...?"
- Use humor and enthusiasm

### Inclusivity
- Explain jargon (kernel, environment, etc.)
- Don't assume prior knowledge
- Use examples that resonate (different fields/interests)
- Offer help without making anyone feel bad
- Acknowledge different ways of learning

### Pacing
- Watch the room for confusion
- Go slower than you think necessary
- Build in "think time" after questions
- It's okay if you don't cover everything

### Technical backup
- Have a second laptop with Jupyter ready
- Have terminal open; be comfortable with command line
- Know how to restart services if something breaks
- Have its-hpc@pomona.edu contact info for emergencies

## Resources for Instructors

- Jupyter documentation: https://jupyter.org/
- Pandas documentation: https://pandas.pydata.org/
- Matplotlib tutorial: https://matplotlib.org/stable/tutorials/
- Software Carpentries teaching tips: https://carpentries.org/
- Sagehen HPC info: https://pomona-college-hpc.github.io/

## Common Learner Questions

**Q: "Can I use Jupyter for production code?"**
A: "Jupyter is best for development and exploration. For code running 24/7 or processing huge datasets, convert to Python scripts and submit as SLURM batch jobs (covered briefly in Episode 6)."

**Q: "What's the difference between JupyterLab and Jupyter Notebook?"**
A: "JupyterLab is the newer interface with better file browsing and tabs. Jupyter Notebook is the older interface. We use JupyterLab; it's better."

**Q: "Can I use Jupyter with R or other languages?"**
A: "Yes! Jupyter supports Python, R, Julia, and 100+ languages through kernels. This workshop focuses on Python, but the same concepts apply."

**Q: "How do I make my notebook faster?"**
A: "Consider: smaller datasets (sample), vectorized operations (NumPy), or batch jobs for heavy lifting. We don't dive deep here, but ask if you need ideas."

**Q: "Is Jupyter suitable for machine learning?"**
A: "Great for developing and testing ML code. For training large models, convert to scripts and run as batch jobs."

**Q: "How do I collaborate using notebooks?"**
A: "Share environment.yml and Git repository. Both people have the same environment and can run each other's notebooks. For real-time collaboration, see nbcollab or Jupyter Hub."

## Final Notes

- This is an introduction; it's okay if learners don't master everything
- The goal is confidence and understanding concepts
- Provide reference materials for later learning
- Create a safe environment to ask questions
- Remember: Everyone started as a beginner. Be patient and encouraging.

Good luck with your workshop!
