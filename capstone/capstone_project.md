# CS383 Capstone Project — Full Pipeline, Your Choice of Problem

**Individual project.** Pick a real-world problem you care about, find real public data to answer it, and
carry it through all 8 steps of the data science workflow we've used all semester — from defining the
problem to presenting your results.

This is the same 8-step workflow from Lecture 1, the same "real data, not toy data" standard the whole
course has been built on, and a chance to apply everything from SQL/Pandas cleaning through model
evaluation and tuning to a problem that's actually yours.

---

## Requirements

**Data must be real, public data.** NYC/NYS Open Data, data.gov, a public agency API, or a similarly
sourced public dataset. No Kaggle-curated, pre-cleaned classroom datasets, or toy sets (Iris, Titanic,
MNIST, etc.) — the whole point is practicing on data nobody has already cleaned up for you.

**This is individual work.** You're responsible for all 8 steps yourself, start to finish.

**Your project must include:**

1. A clearly defined, answerable question — a regression or classification problem (not just "explore
   this dataset")
2. Real data cleaning work — your dataset needs to actually require it (missing values, inconsistent
   formatting, needed joins, etc.)
3. Exploratory data analysis with at least one meaningful visualization
4. At least one trained model, compared against a simple baseline (e.g., majority-class or mean prediction)
5. Evaluation using metrics appropriate to your problem type (not just accuracy if your classes are
   imbalanced — you know why by now)
6. At least one documented attempt to improve your model (feature changes, different algorithm,
   hyperparameter tuning, etc.) and what happened when you did
7. A short **ethics and limitations reflection** — see below
8. A plain-language summary a non-technical reader could understand, plus a short presentation
9. A **live, working deployment** of your model — see below

---

## Live deployment (required)

Your model needs to be reachable at a public URL where someone who has never seen your notebook can type
in some values and get a real prediction back. This is what turns your capstone from "a project I did for
a class" into something you can actually put on a resume and invite someone to click.

Full step-by-step instructions — saving your model, building a small app, and deploying it for free — are
in the separate **[Capstone Deployment Guide](capstone_deployment_guide.md)**. Start that process well
before Week 15; deployment issues are much easier to debug with time to spare.

Your final submission must include the live URL, and it must actually work when your instructor tries it.

---

## The ethics and limitations reflection (required)

As part of Step 8, include a short written section addressing:

- Who is represented in your data, and who might not be? Could that affect your model's predictions for
  different groups?
- If this model were actually deployed and relied on, what's the realistic worst case if it's wrong?
- What would you want to test or verify before trusting this model's predictions in a real decision?

This doesn't need to be long, but it needs to be specific to *your* data and *your* model — generic
statements about "AI bias" without engaging with your actual project won't satisfy this requirement.

---

## Timeline

| Milestone | Due |
|---|---|
| **Proposal** — your topic, dataset source (with a link), and the specific question you want to answer (one paragraph) | End of **Week 5** |
| **Progress check** — a short notebook showing your cleaned data and initial EDA, even if your model isn't built yet | End of **Week 11** |
| **Final notebook + presentation** | **Week 15** |

Proposals need instructor approval before you start building — this mainly checks that your data source
is real, accessible, and that your question is answerable with it. Submit both the proposal and progress
check on BrightSpace under their respective assignment entries.

---

## Deliverables

1. **A Jupyter notebook** containing your full pipeline, organized into 8 clearly labeled sections
   mirroring the workflow above. Use markdown throughout to explain your reasoning at each step — this
   should read as a story, not just a sequence of code cells.
2. **A live deployed app** at a public URL (see the [Capstone Deployment Guide](capstone_deployment_guide.md)),
   plus the public GitHub repo it's deployed from.
3. **A short presentation** during Week 15 covering your problem, approach, and findings (length and
   format details will be shared closer to the date).

Submit your final notebook, GitHub repo link, and live app link on BrightSpace under **Capstone Project**
before your presentation.
