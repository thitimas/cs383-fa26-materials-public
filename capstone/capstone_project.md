# CS383 Capstone Project — Full Pipeline, Your Choice of Problem

This is an individual project. Pick a real-world problem you care about, find real public data to answer
it, and carry it through the same 8-step data science workflow we've used all semester — from defining
the problem to communicating what you found. On top of the notebook, you'll also deploy your model as a
small live app that anyone can try.

This project is meant to be something you can genuinely be proud of and show off — in an interview, on a
resume, or to a future employer. Take the extra time to make it something you'd want to talk about.

---

## The 8-Step Workflow

Your notebook should be organized around these eight steps, in this order, using these names:

1. Define the problem
2. Collect data
3. Clean the data
4. Explore the data
5. Build a model
6. Evaluate the model
7. Improve the model
8. Communicate the findings

Live deployment is a separate deliverable on top of these eight steps, not a ninth step in the notebook —
more on that below.

---

## Where your data comes from

Your dataset must come from a **credible, identifiable public source** — NYC/NYS Open Data, Data.gov, a
public agency API, or a research data repository are all good examples.

Kaggle is not automatically acceptable as your source. If a dataset happens to live on Kaggle, you need
to track down and cite the *original, authoritative source* it came from, and the data still has to
require meaningful preparation on your part. "I downloaded a clean CSV from Kaggle" is not a valid
project starting point.

Pre-cleaned classroom datasets and toy datasets (Iris, Titanic, MNIST, and similar) remain prohibited.

A few things every project needs to satisfy:

- Your dataset must require **meaningful cleaning or integration work** — the whole point is practicing
  on data nobody has already cleaned up for you
- Include the **source link** in your notebook
- Briefly describe the dataset's **provenance** — who collected it, when, and for what original purpose

### Gathering data at scale

You're welcome to pull a genuinely large dataset yourself rather than working from a single static file —
in fact, this often makes for a stronger project, since assembling the data *is* real work worth showing.

The most reliable way to do this is the same pattern used throughout this course: a public agency API on
the Socrata platform (NYC Open Data and many state/city portals run on this). A single request usually
caps out around 1,000-50,000 rows depending on the endpoint, so pulling a full dataset means paginating
with `$limit` and `$offset` in a loop, not one giant request. Registering for a free Socrata app token is
worth doing if you're pulling a lot of data — unauthenticated requests get throttled harder.

Once you've pulled it, save it to a local CSV and read from that file for the rest of your notebook,
rather than re-querying the API on every run — the same live-pull-with-local-fallback pattern you've seen
in every lecture this semester.

If your full pull ends up large (hundreds of thousands of rows or more), keep it as your genuine "collected
data" for Step 2, then document an explicit, reasoned sample before modeling in Step 5 — collect big, model
small, and say so directly in your notebook. Don't discard the scale of what you gathered just because you
have to downsample it later; the full pull is still real evidence of the collection work.

**A caution on web scraping:** pulling from a documented, official API (like Socrata above) is fine.
Scraping raw HTML from an arbitrary website is a different thing — it raises real terms-of-service and
legal questions depending on the site, it's fragile (a single layout change breaks your whole pipeline),
and it isn't a tool this course has taught you. If your project idea seems to require scraping a page
that has no API, talk to your instructor before building around it — there's often an official data
source underneath that you just haven't found yet.

---

## Notebook requirements, step by step

### Step 1 — Define the problem

- A specific, answerable question — not just a topic ("predict whether a 311 complaint will take more
  than 24 hours to resolve," not "look at 311 data")
- Clearly state whether this is a **classification** or **regression** problem
- Clearly identify and explain your **target variable** and the **features** you plan to use, and why
  each feature is relevant to the question

### Step 2 — Collect data

- Data pulled or loaded directly in your notebook, from the public source described above
- A quick look at what you're working with — size, columns, and data types

### Step 3 — Clean the data

- Address real issues in your data — missing values, inconsistent formatting, duplicates, or joins across
  multiple sources
- Explain each cleaning decision in markdown as you go, including your reasoning (why drop vs. fill vs.
  flag)

### Step 4 — Explore the data

- At least one meaningful, well-labeled visualization
- Your EDA findings should actually inform your later choices — which features to use, which model might
  fit, what to expect from your baseline

### Step 5 — Build a model

- Your algorithm must be one we've covered in class:
  - **Regression:** Linear Regression, Ridge/Lasso
  - **Classification:** Logistic Regression, k-NN, Decision Tree, Random Forest, XGBoost
  - (Decision Tree, Random Forest, and XGBoost also have regressor versions, if your problem is regression)
  - No neural networks, deep learning, or other tools we haven't covered — this project is about showing
    what *you* learned this semester, not what a library can do on its own. If you're not sure whether
    something counts, ask before you build around it.
- Create your **train/test split before** any model development begins, with a fixed `random_state`
- Do all preprocessing, feature selection, and hyperparameter tuning using **only the training data** —
  your test set should not influence any decision you make along the way
- Train a simple **baseline** (majority-class or mean prediction) so you have something real to compare
  against
- Keep it running fast: our JupyterHub is a CPU-only pilot service, so your model needs to train in a few
  minutes, not tens of minutes. If your full dataset is large, sample it down to something manageable and
  say so directly in your notebook

### Step 6 — Evaluate the model

- Use your **test set only for final evaluation** — not something you check back on repeatedly while
  still tuning your model. Repeatedly peeking at test performance while developing is itself a form of
  overfitting.
- Use metrics appropriate to your problem type (not accuracy alone on an imbalanced classification
  problem, not R² alone for regression)
- Build a clear **results table** comparing your baseline, your initial model, and your improved model
  side by side
- Explain what your metrics actually mean *in the context of your problem* — not just "the F1 score was
  0.82," but what that means for whoever would actually use this prediction

### Step 7 — Improve the model

- At least one genuine, documented improvement attempt — different features, a different algorithm,
  hyperparameter tuning, or similar
- Report what happened, including if it **didn't help**. A well-documented attempt that failed and was
  properly interpreted counts for full credit — this is more valuable than an unexplained model with no
  iteration shown at all
- Briefly discuss **possible data leakage** in your pipeline and specifically how you prevented it (for
  example: fitting a scaler only on training data, not letting future information leak into features)

### Step 8 — Communicate the findings

- A plain-language summary a non-technical reader could actually follow
- Your conclusion should **directly answer the question you posed in Step 1** — don't let the notebook
  trail off into just describing what you did
- Distinguish **predictive performance from real-world usefulness** — a model can score well and still not
  be something anyone should actually rely on
- Don't make **causal claims** ("X causes Y") unless your project's design actually supports that kind of
  claim — most of these projects will only support correlational or predictive statements, and that's
  fine, just be honest about which one you have
- An **ethics and limitations reflection** — see below

---

## Ethics and limitations reflection

As part of Step 8, include a short written section addressing:

- Who is represented in your data, and who might not be? Could that affect your model's predictions for
  different groups?
- If this model were actually deployed and relied on, what's the realistic worst case if it's wrong?
- What would you want to test or verify before trusting this model's predictions in a real decision?

This doesn't need to be long, but it needs to be specific to *your* data and *your* model — generic
statements about "AI bias" without engaging with your actual project won't satisfy this requirement.

---

## Live deployment

Your model needs to be reachable at a public URL where someone who has never seen your notebook can enter
some values and get a real prediction back.

The bar here is functional, not polished:

- The app just needs to **load, accept reasonable inputs, and return a real prediction** from your
  trained model
- **Visual design is not a major grading criterion.** A plain, working app beats a beautiful, broken one
- Include **basic input validation** (reasonable ranges, sensible defaults) and **understandable feature
  labels** — someone unfamiliar with your notebook should be able to tell what each input means
- Your app must display a short statement that it is an **educational project**, and should not be used
  for actual medical, legal, financial, employment, or public-safety decisions
- If your project topic is inherently high-stakes (health outcomes, criminal justice, hiring, and similar),
  you need **prior instructor approval** before building around it

**If your hosting platform has a documented outage** at the time of grading, your instructor will evaluate
your app locally by running it directly from your submitted GitHub repository instead — this is why your
repo needs to include everything necessary to run the app locally (see the deployment guide).

Full step-by-step instructions — saving your model, building the app, and deploying it for free — are in
the separate **[Capstone Deployment Guide](capstone_deployment_guide.md)**. Start this process well
before Week 15; deployment issues are much easier to debug with time to spare.

---

## Using generative AI

You're welcome to use generative AI tools (like Claude, ChatGPT, or GitHub Copilot) for brainstorming,
debugging, explaining unfamiliar code, or improving the clarity of your writing. A few ground rules:

- You're responsible for **understanding and verifying everything you submit**, regardless of how it was
  produced
- If you used AI for anything substantial (not just a quick syntax question), include a short appendix
  at the end of your notebook naming the tool, how you used it, and what you changed or verified afterward
- Be ready to **explain your code, modeling decisions, results, and any AI-assisted work** during your
  presentation
- AI-generated work you can't explain yourself won't receive credit — this applies whether or not it was
  disclosed

---

## Timeline

| Milestone | Due |
|---|---|
| Proposal and dataset approval | Week 5 |
| Data and target verification | Week 7 |
| Cleaning and initial EDA | Week 9 |
| Progress check and baseline model | Week 11 |
| Improved model and evaluation | Week 13 |
| Deployment check | Week 14 |
| Final submission and presentation | Week 15 |

The intermediate checkpoints (Weeks 7, 9, 13, and 14) can be brief — a short notebook excerpt or a couple
sentences showing you're on track is enough. Weeks 5, 11, and 15 are the substantial milestones. Submit
each checkpoint on BrightSpace under its own assignment entry.

---

## Deliverables

1. **A Jupyter notebook** containing your full pipeline, organized into the 8 clearly labeled sections
   above. Use markdown throughout to explain your reasoning at each step — this should read as a story,
   not just a sequence of code cells. Your submitted notebook must **run from beginning to end without
   errors** (Restart Kernel → Run All Cells, with no failures).
2. **A public GitHub repository** containing your notebook, your app code, and everything needed to run
   your app locally if needed.
3. **A live deployed app** at a public URL (see the [Capstone Deployment Guide](capstone_deployment_guide.md)).
4. **A short presentation** during Week 15 covering your problem, approach, and findings (length and
   format details will be shared closer to the date).

Submit your final notebook, GitHub repo link, and live app link on BrightSpace under **Capstone Project**
before your presentation.

---

## Grading

| Category | Weight |
|---|---|
| Problem definition and data source | 10% |
| Data cleaning and preparation | 15% |
| EDA and visualization | 15% |
| Modeling and baseline comparison | 20% |
| Evaluation and model improvement | 15% |
| Interpretation, ethics, and limitations | 10% |
| Notebook organization and reproducibility | 5% |
| Live deployment and GitHub repository | 5% |
| Presentation | 5% |

---

Questions about your topic, your data source, or anything in this prompt? Ask early — it's much easier to
adjust course in Week 5 or 7 than in Week 13.
