# Capstone Deployment Guide — Making Your Model Live

Your capstone isn't finished when your notebook runs — it's finished when someone else can open a link,
type in some values, and get a real prediction from your actual trained model. That's the difference
between "a project for a class" and "a project you can put in front of a recruiter and say: try it
yourself."

This guide walks through the simplest path: **Streamlit Community Cloud**. It's free, requires no credit
card or server management, and works well for the kind of tabular prediction problems most capstones in
this course will build (predict a number or a category from a handful of input values).

If your project is text-based (like the Hugging Face bias-audit style projects), see the note on
**Hugging Face Spaces** at the end — it's a better fit for that kind of project specifically.

---

## What you're building

A small web app with:
- A few input boxes/dropdowns matching your model's features
- A button that runs your trained model on those inputs
- The prediction displayed back to the user

That's it. It doesn't need to be fancy — it needs to actually work.

---

## Step 1 — Save your trained model to a file

Right now your model only exists inside your notebook's memory. You need to save the actual fitted model
object to a file, so your deployed app can load it without retraining from scratch every time someone
visits.

Add this near the end of your notebook, right after you've trained your final model:

```python
import joblib

joblib.dump(model, "model.joblib")
```

This creates a file called `model.joblib` in the same folder as your notebook. Confirm it actually
appears there before moving on.

---

## Step 2 — Create `app.py`

This is a separate Python file (not a notebook) that Streamlit will run. Create a new file named
`app.py` in the same folder, and adapt this template to your actual features:

```python
import streamlit as st
import joblib
import pandas as pd

# Load your trained model
model = joblib.load("model.joblib")

st.title("My Capstone: [Your Project Name]")
st.write("Enter values below to get a prediction from my trained model.")

# --- Replace these with YOUR actual features ---
feature1 = st.number_input("Feature 1 name", value=0.0)
feature2 = st.selectbox("Feature 2 name", ["Option A", "Option B", "Option C"])
feature3 = st.slider("Feature 3 name", min_value=0, max_value=100, value=50)
# -------------------------------------------------

if st.button("Predict"):
    input_df = pd.DataFrame(
        [[feature1, feature2, feature3]],
        columns=["feature1", "feature2", "feature3"],  # must match your training column names/order
    )
    prediction = model.predict(input_df)
    st.success(f"Prediction: {prediction[0]}")
```

A few things that matter here:

- The column names and order in `input_df` must exactly match what your model was trained on. If your
  model used one-hot encoding or scaling, you need to apply the same preprocessing to `input_df` before
  calling `.predict()` — consider saving your preprocessing pipeline (scaler, encoder) with `joblib` too,
  the same way you saved the model.
- Pick input widgets (`st.number_input`, `st.selectbox`, `st.slider`, `st.text_input`) that match each
  feature's actual data type.

---

## Step 3 — List your dependencies in `requirements.txt`

Create a file named `requirements.txt` (no code, just a plain list) with every package your `app.py`
needs:

```
streamlit
scikit-learn
pandas
joblib
```

Add any other library your model or preprocessing depends on (e.g. `xgboost` if you used it).

---

## Step 4 — Push everything to a public GitHub repo

Your repo needs at least these four files in it:

```
your-capstone-repo/
├── app.py
├── model.joblib
├── requirements.txt
└── README.md
```

(Your full analysis notebook can live in the same repo too — it should, so people can see your full
process, not just the app.)

```bash
git init
git add app.py model.joblib requirements.txt README.md your_notebook.ipynb
git commit -m "Capstone project"
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git
git push -u origin main
```

**This repo must be public** — Streamlit Community Cloud needs to read it, and a recruiter needs to be
able to see it too.

---

## Step 5 — Deploy on Streamlit Community Cloud

1. Go to **[share.streamlit.io](https://share.streamlit.io)** and sign in with your GitHub account (free).
2. Click **New app**.
3. Choose your repository, the branch (usually `main`), and the file path (`app.py`).
4. Click **Deploy**.

The first deploy takes a few minutes while it installs your `requirements.txt`. Once it's done, you'll
get a live public URL that looks like:

```
https://your-app-name.streamlit.app
```

Open it yourself and actually test it — type in real values and confirm you get a real prediction back,
not an error.

---

## Step 6 — Link it everywhere

- Add the live URL to the top of your GitHub repo's `README.md`
- Add it to your final notebook
- This is the link you'll put on your resume/LinkedIn, not the GitHub repo link alone — a working demo
  people can click is worth more than a link to code they'd have to run themselves

---

## Troubleshooting

**App won't start / shows a red error box.** Almost always a missing package — check that everything
your `app.py` imports is listed in `requirements.txt`, with correct spelling.

**"File not found: model.joblib."** Confirm `model.joblib` was actually committed and pushed to your
GitHub repo, not just sitting on your own computer — check the file list on your repo's GitHub page.

**Prediction looks wrong or crashes.** Almost always a mismatch between the column names/order you used
when training versus the column names/order in `app.py`'s `input_df`. Print `model.feature_names_in_`
in your notebook to double check the exact names and order your model expects.

**Model file is huge / repo push fails.** If `model.joblib` is larger than 100MB, GitHub will reject the
push. This shouldn't happen for the kinds of models this course builds — if it does, come talk to your
instructor rather than trying to work around it.

---

## Alternative: Hugging Face Spaces (better fit for text-based projects)

If your capstone is text/NLP-based rather than predicting from tabular features, **Hugging Face Spaces**
with **Gradio** is a more natural fit and is arguably more recognized specifically within ML-focused
recruiting than Streamlit:

1. Create a free account at [huggingface.co](https://huggingface.co).
2. Go to **Spaces** → **Create new Space** → choose **Gradio** as the SDK.
3. This gives you a Space with a `git` repo you push to, similar to Steps 3–4 above, except your app file
   is `app.py` using `gradio` instead of `streamlit` (e.g. `import gradio as gr`).
4. Push your model file, `app.py`, and `requirements.txt` the same way. The Space builds and hosts itself
   automatically — no separate deploy step.

Ask your instructor before switching to this path if you're not sure which one fits your project better.
