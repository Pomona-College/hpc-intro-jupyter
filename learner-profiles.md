---
title: Learner Profiles
---

## Typical Participants

This workshop is designed for researchers and students at Pomona College who want to use interactive Python notebooks for data analysis on the Sagehen HPC cluster. Here are typical learner profiles:

### Profile 1: Graduate Student Moving from Laptop to Cluster

**Name:** Sam Chen
**Background:** 2nd-year master's student in biology

**Motivation:**
- Currently uses Jupyter on laptop for analyzing small datasets (< 5 GB)
- Dataset just grew to 100 GB; laptop can't handle it
- Wants to keep using Jupyter (loves the interactive environment)
- Wants data to live on cluster; doesn't want to download/upload files
- Needs to finish research; wants minimal setup time

**Experience:**
- Proficient in Python (pandas, matplotlib, numpy)
- Uses Jupyter extensively (has 20+ notebooks from coursework)
- Tried command-line HPC once; it was intimidating
- Comfortable with file systems and basic computing concepts

**Pain Point:**
"I love Jupyter for my analysis, but my laptop is too slow now. The cluster is powerful but I don't want to learn command-line tools. Can't I just use Jupyter directly?"

**Expected Outcome After Workshop:**
- Successfully launch JupyterLab on Sagehen via OnDemand
- Load data directly from /bigdata (lab storage)
- Run analysis interactively using cluster resources
- Understand how to manage Python environments for reproducibility
- Know when to use Jupyter vs. batch jobs

**Preferences:**
- Python; heavy data analysis
- Needs quick setup (no deep learning curve)
- Cares about reproducibility (will be published)

---

### Profile 2: Faculty Member Teaching with Jupyter

**Name:** Dr. Priya Patel
**Background:** Assistant Professor of Environmental Science

**Motivation:**
- Teaches undergraduate course on environmental data analysis
- Currently uses Jupyter locally with small datasets
- Wants to scale to real-world, large datasets for teaching
- Wants to show students how professional research uses HPC
- Wants to demonstrate Jupyter as a reproducible science tool

**Experience:**
- Expert in environmental science; intermediate Python programmer
- Uses Jupyter in teaching; students love it
- Never used HPC clusters
- Linux-comfortable from grad school but rusty

**Pain Point:**
"My students learn data analysis with toy datasets. I want them to work with real climate or geological data, but my laptop and OnDemand storage can't handle it. If I could show them HPC+Jupyter, they'd understand scalable research better."

**Expected Outcome After Workshop:**
- Set up Jupyter on Sagehen for course use
- Create reproducible course materials and example notebooks
- Use large datasets in teaching
- Know how to create shared environments for students
- Understand enough to debug student issues

**Preferences:**
- Wants clean, documented examples
- Values reproducibility and pedagogy
- Needs to be able to explain to students

---

### Profile 3: Postdoc Using HPC for First Time

**Name:** Alex Martinez
**Background:** Postdoctoral researcher in computational chemistry

**Motivation:**
- Moved to Pomona; has access to Sagehen for first time
- Previously ran simulations on smaller university cluster
- Eager to use more resources for research
- Wants an interactive way to analyze simulation results
- Heard about Jupyter; wants to see if it fits workflow

**Experience:**
- Expert in chemistry and computation (C++, Python coding)
- Used high-performance computing before (but on different cluster)
- First time using Jupyter (has seen Colab; interested in the real version)
- Comfortable with command-line tools but prefers GUIs when available

**Pain Point:**
"I can write and run simulations, but analyzing results is painful. I download files locally, load in Jupyter, analyze. I want a faster feedback loop where I can analyze on the cluster where data lives."

**Expected Outcome After Workshop:**
- Understand Jupyter workflow on HPC
- Know how to launch Jupyter with specific resource requests (GPU, cores)
- Learn to create reproducible environments for research
- Understand when Jupyter fits and when batch jobs are better
- Be able to teach new students in lab

**Preferences:**
- Wants technical depth (understands HPC concepts)
- Will push system to the limit (GPU work, large analyses)
- Cares about efficiency and reproducibility

---

## Common Learner Characteristics

### Technical Background

**What learners typically know:**
- Basic to intermediate Python (variables, functions, libraries)
- How to use a Jupyter Notebook locally (on laptop)
- Basic file systems and directory navigation
- What HPC clusters are (conceptually)

**What they often struggle with:**
- Linux command-line (if not used recently)
- Module systems (like Lmod)
- SLURM job submission
- Understanding when to use interactive vs. batch
- Environment management and dependencies

**What they don't know:**
- How OnDemand works
- How to manage conda environments properly
- Best practices for reproducible notebooks
- How to scale from Jupyter to production

### Motivations

Learners are motivated by:

1. **Problem-solving**: They have research data they want to analyze quickly
2. **Productivity**: They want to minimize setup time and learn one tool
3. **Scalability**: Their laptop can't handle their data anymore
4. **Reproducibility**: They care about sharing work with collaborators
5. **Learning**: They're curious about HPC and interactive computing

They are **not** motivated by:

- Learning for learning's sake (they have real work to do)
- Deep technical details (unless relevant to their research)
- Anything that takes time away from their research

### Fears and Concerns

Common worries:

- **"Will I break something?"**: Anxiety about cluster permissions
- **"Is this too hard?"**: Worry about command-line work
- **"Will I lose my data?"**: Concern about file safety
- **"Will it be slow?"**: Concern about network/cluster delays
- **"Can I do my actual work?"**: Skeptical that Jupyter can handle real data

### Learning Preferences

Learners prefer:

- **Hands-on practice** over slides
- **Real examples** over toy data
- **Clear documentation** over deep theory
- **Quick wins** ("I ran my first notebook in 10 minutes!")
- **Relevance** ("This applies to my research")

---

## Workshop Design Philosophy

This workshop is built around these learner profiles:

1. **Hands-on from the start**: Episode 2 has learners launch Jupyter immediately
2. **Real data examples**: Data analysis examples use realistic datasets
3. **Problem-focused**: Motivation comes from their research pain points
4. **Modular content**: Learners can skip ahead if they have prior experience
5. **Reproducibility emphasis**: Best practices thread throughout
6. **Graduate-student paced**: Not too slow (they're busy) but not too fast

## Accessibility Considerations

The workshop accommodates diverse learners:

- **Visually**: Large, clear text in notebooks; color-independent plots
- **Auditory**: Captions if videos used; written transcripts of demos
- **Motor**: Keyboard alternatives; no fast-paced typing required
- **Cognitive**: Clear language; step-by-step instructions; breaks
- **Internet**: Content available offline; contingency plans if cluster down

Materials are available in multiple formats:

- Web pages (this workshop site)
- Printable reference card (PDF)
- Video recordings (optional, for asynchronous learning)
- Plain-text setup guide
- Email summaries for those who prefer async participation

## Diversity and Inclusion

We recognize participants come from different backgrounds:

- **Different fields** (biology, chemistry, physics, geology, CS, statistics, economics, etc.)
- **Different experience levels** (undergrad to faculty)
- **Different comfort with computing** (some are CS experts; others are not)
- **Different ways of learning** (visual, kinesthetic, reading/writing, etc.)
- **Different languages and cultures** (we use plain English; we're respectful)

The workshop:

- Uses examples from multiple fields
- Never assumes prior knowledge
- Explains jargon clearly
- Welcomes all questions
- Provides multiple ways to learn (live demo, written guide, hands-on practice)
- Is an inclusive, judgment-free space

---

## Summary

The "typical" learner for this workshop:

✓ Has Python experience and has used Jupyter locally
✓ Has HPC account but hasn't used clusters interactively
✓ Wants to use Jupyter on Sagehen with real data
✓ Values productivity and reproducibility
✓ Wants hands-on learning with real examples
✓ Is motivated by their own research

This workshop is **for them**, and designed to solve their actual problems.
