# CS383 — Fall 2026 Public Materials

Public, student-facing materials for CS383 (Data Science and Machine Learning),
published via GitHub Pages. Solutions, Otter Grader assignments, and instructor
notes live in a separate private repo — nothing here should ever include
answer keys.

## Structure

```
cs383-fa26-materials-public/
├── index.html                                          (course landing page)
├── lect01/
│   ├── lect01_intro_to_ds_ml_live.ipynb               (live in-class version)
│   ├── lect01_intro_to_ds_ml_exercise.ipynb           (reflection + optional challenge)
│   ├── thai_character_activity.html                   (unplugged activity)
│   └── unsupervised_sorting_activity.html             (unplugged activity)
├── lect02/
│   ├── lect02_python_numpy_vectorization_live.ipynb
│   └── lect02_python_numpy_vectorization_exercise.ipynb
├── lect03/
│   ├── lect03_pandas_sql_fundamentals_live.ipynb
│   ├── lect03_pandas_sql_fundamentals_exercise.ipynb
│   └── lect03_inclass_exercise_joins.ipynb
├── lect04/
│   ├── lect04_datetime_cleaning_reshaping_live.ipynb
│   ├── lect04_datetime_cleaning_reshaping_exercise.ipynb
│   └── assignment1_restaurant_inspections.ipynb        (graded assignment)
└── lect05/
    ├── lect05_eda_statistics_live.ipynb
    ├── lect05_eda_statistics_exercise.ipynb
    └── images/                                         (reference figures used in the live notebook)
```

Every `_exercise.ipynb` notebook is fill-in-the-blank practice (`__________`
marks each blank) with a self-contained setup and an Optional Challenge at
the end — no answers included.

Every `_live.ipynb` notebook is the lecture notebook with one `__________`
blank per teaching moment, meant to be typed along with in class; setup,
boilerplate, and demo-only cells are left filled in so class time stays on
the new syntax. New `lectXX/` folders get added as each lecture's
public-facing material is ready.

## Live links

- Course landing page: https://thitimas.github.io/cs383-fa26-materials-public/
- Lecture 1, supervised learning activity: https://thitimas.github.io/cs383-fa26-materials-public/lect01/thai_character_activity.html
- Lecture 1, unsupervised learning activity: https://thitimas.github.io/cs383-fa26-materials-public/lect01/unsupervised_sorting_activity.html

## Publishing a new page

1. Add the file under the right `lectXX/` folder.
2. `git add -A && git commit -m "Lecture XX: <what was added>" && git push`
3. GitHub Pages rebuilds automatically after each push to `main` (usually live within a minute or two).
