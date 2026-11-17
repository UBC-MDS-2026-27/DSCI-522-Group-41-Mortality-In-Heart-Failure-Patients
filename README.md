# Predicting Student Depression Using Demographic, Academic, and Lifestyle Factors

<!-- TODO: adjust the title so it matches your final question. -->

**Authors:** Linda Arthur, Luis Mario, Yunpeng Xie

**Rendered report:** [View the report](https://ubc-mds-2026-27.github.io/DSCI-522-Group-41-Student-Depression-Classifier-/)
<!-- TODO: replace with your real GitHub Pages URL and click it to confirm it works. -->

## Summary

In this project, we ask whether we can predict if a university student reports
depression from their demographic, academic, social and health characteristics,
such as age, gender, Cumulative Grade Point Average (CGPA), current semester,
friend circle, living arrangement and family background. We use the Student
Depression Detection Dataset, a survey of 4,464 students aged 17 to 28, of whom
about 27% report depression. We train a logistic regression model to classify
each student as reporting depression or not, and we evaluate it on a held-out
test set using recall and F1 score, since failing to identify a student at risk
is more costly than a false alarm.

> **Work in progress:** We are currently building and evaluating the model.
> This section will be updated with our high-level findings and one or two
> sentences on what they might mean once the analysis is complete. Because the
> data record self-reported depression rather than a clinical diagnosis, any
> model we build is intended as a screening aid, not a diagnostic tool.

## Data

The data come from the
[Student Depression Detection Dataset](https://www.kaggle.com/datasets/mkhoirulmustaqim/student-depression-detection-dataset)
on Kaggle (TODO: author name, year). Each row represents one student who
answered the survey, and the target variable is `Depression` (TODO: confirm the
exact column name and its values, e.g., Yes/No).

<!--
TODO: confirm from the data card the number of rows and columns, the license,
and the original source. If the data come from another repository (e.g.,
Mendeley Data), cite that original source as well.
-->

## How to run the analysis

The following steps work on both Windows and macOS.

### 1. Install the required tools

Install [uv](https://docs.astral.sh/uv/getting-started/installation/) and
[Quarto](https://quarto.org/docs/get-started/) if you do not already have them.

### 2. Clone the repository

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-41-Student-Depression-Classifier-.git
cd DSCI-522-Group-41-Student-Depression-Classifier-
```

### 3. Set up the environment

```bash
uv sync
```

### 4. (Only if the data are downloaded from Kaggle) Set up a Kaggle API token

<!--
The milestone requires that the README walks through obtaining and setting up
any API token if the data source requires authentication. Delete this section
if you download the data from an open source that does not need a login.
-->

1. Sign in to [Kaggle](https://www.kaggle.com), go to **Settings**, and under
   **API** click **Create New Token**. This downloads a file named
   `kaggle.json`.
2. Move the file to the location Kaggle expects:
   - macOS: `~/.kaggle/kaggle.json`
   - Windows: `C:\Users\<your-username>\.kaggle\kaggle.json`

### 5. Run the analysis and render the report

```bash
uv run quarto render analysis/student_depression_analysis.qmd
```

<!-- TODO: use the exact name of your .qmd file. -->

The rendered report will be saved as
`analysis/student_depression_analysis.html`. Running the report downloads the
raw data to `data/raw/` and writes the cleaned data to `data/processed/`.

## Dependencies

- [uv](https://docs.astral.sh/uv/) for managing the Python environment
- [Quarto](https://quarto.org/) for rendering the report
- Python packages and their versions are listed in
  [`pyproject.toml`](pyproject.toml) and pinned in [`uv.lock`](uv.lock)

## Licenses

The software code in this repository is licensed under the MIT License, and
the report is licensed under the Creative Commons
Attribution-NonCommercial-NoDerivatives 4.0 International License
(CC BY-NC-ND 4.0). See [`LICENSE.md`](LICENSE.md) for the full text.

<!-- TODO: these names must match exactly what is in LICENSE.md. -->

## Use of generative AI

<!--
State whether generative AI was used and how. If you used instruction files
(e.g., CLAUDE.md), commit them and link to them. Include a few example prompts.
-->

We used TODO (e.g., Claude) to help draft the structure of this README and to
review parts of our code. All AI suggestions were reviewed, edited and approved
by team members, who remain responsible for the final content. Our instruction
file is available at [`CLAUDE.md`](CLAUDE.md) (TODO: remove this sentence if not
used).

Example prompts we used:

- "Help me give a structure to the README using the Milestone 1 requirements and
  the information from my dataset."
- TODO
- TODO

## Contributing and code of conduct

If you would like to contribute, please read [`CONTRIBUTING.md`](CONTRIBUTING.md).
Everyone participating in this project is expected to follow our
[`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).
