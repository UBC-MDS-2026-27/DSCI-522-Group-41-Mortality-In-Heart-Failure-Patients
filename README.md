# Predicting Student Depression Using Demographic, Academic, and Lifestyle Factors

**Authors:** Linda Arthur, Luis Mario, Yunpeng Xie

**Rendered report:** [View the report](https://ubc-mds-2026-27.github.io/DSCI-522-Group-41-Student-Depression-Classifier-/)

## Summary

In this project, we ask whether we can predict if a university student reports
depression from their demographic, academic, social and health characteristics,
such as age, gender, Cumulative Grade Point Average (CGPA), current semester,
friend circle, living arrangement and family background. We use the
[Student Depression Detection Dataset](https://www.kaggle.com/datasets/mkhoirulmustaqim/student-depression-detection-dataset),
a survey of 4,464 students aged 17 to 28, of whom about 27% report depression.
We train a logistic regression model to classify each student as reporting
depression or not, and we evaluate it on a held-out test set using recall and
F1 score, since failing to identify a student at risk is more costly than a
false alarm.

> **Work in progress:** We are currently building and evaluating the model.
> This section will be updated with our high-level findings and one or two
> sentences on what they might mean once the analysis is complete. Because the
> data record self-reported depression rather than a clinical diagnosis, any
> model we build is intended as a screening aid, not a diagnostic tool.

## How to run the analysis

These steps work on both Windows and macOS. First, install
[uv](https://docs.astral.sh/uv/getting-started/installation/) and
[Quarto](https://quarto.org/docs/get-started/). The data are downloaded from
Kaggle, so you also need a Kaggle API token: sign in to Kaggle, go to
**Settings**, click **Create New Token** under **API**, and save the downloaded
`kaggle.json` file to `~/.kaggle/kaggle.json` on macOS or
`C:\Users\<your-username>\.kaggle\kaggle.json` on Windows.

Then clone the repository, set up the environment and render the report:

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-41-Student-Depression-Classifier-.git
cd DSCI-522-Group-41-Student-Depression-Classifier-
uv sync
uv run quarto render analysis/student_depression_analysis.qmd
```

The rendered report is saved as `analysis/student_depression_analysis.html`.

## Dependencies

The project uses [uv](https://docs.astral.sh/uv/) to manage the Python
environment and [Quarto](https://quarto.org/) to render the report. All Python
packages and their versions are listed in [`pyproject.toml`](pyproject.toml)
and pinned in [`uv.lock`](uv.lock).

## Licenses

The code in this repository is licensed under the MIT License, and the report
is licensed under the Creative Commons Attribution-NonCommercial-NoDerivatives
4.0 International License (CC BY-NC-ND 4.0). See [`LICENSE.md`](LICENSE.md)
for the full text.

## Use of generative AI

We used Claude to help draft the structure of this README. All AI suggestions
were reviewed, edited and approved by team members, who remain responsible for
the final content. 