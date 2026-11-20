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

These steps work on both macOS and Windows.

### 1. Install the tools

Install [uv](https://docs.astral.sh/uv/getting-started/installation/) and
[Quarto](https://quarto.org/docs/get-started/). You do not need to install
Python yourself: uv downloads the version the project uses (Python 3.14, set
in `.python-version`) when you set up the environment.

The data set is included in `data/raw/`. If it is missing, the report
downloads it from the UCI Machine Learning Repository the first time it runs.

### 2. Clone the repository and create the environment

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-41-Mortality-In-Heart-Failure-Patients.git
cd DSCI-522-Group-41-Mortality-In-Heart-Failure-Patients
uv sync
```

`uv sync` creates a `.venv` folder inside the project and installs the exact
package versions pinned in `uv.lock`, including Jupyter, which Quarto needs to
run the Python code. On macOS, `.venv` is hidden in Finder; press
**Cmd + Shift + .** to show hidden folders.

Do not install packages with `pip install` (or with your editor's "install
package" prompt). With the Python that uv manages, pip fails with an
"externally managed environment" error, and packages installed that way are
not recorded for the rest of the team. See
[Adding or removing packages](#adding-or-removing-packages) below.

### 3. Select the project environment in your editor

To run code chunks interactively, your editor must use the project
environment, not your global Python.

**Positron or VS Code**

1. Open the project folder with **File → Open Folder**.
2. Click the interpreter button in the top-right corner (it may say something
   like `Python 3.14.7 (Global)`), or open the Command Palette
   (**Cmd + Shift + P** on macOS, **Ctrl + Shift + P** on Windows) and run
   **Python: Select Interpreter**.
3. Choose the environment named
   `dsci-522-group-41-Mortality-In-Heart-Failure-Patients`.
4. If it is not listed, choose the option to enter an interpreter path and
   give the Python inside the project's `.venv` folder:
   - macOS: `.venv/bin/python`
   - Windows: `.venv\Scripts\python.exe`
5. Restart the Python console.

**JupyterLab:** start it from the project folder with `uv run jupyter lab`.

To check that the environment works, run this in the terminal from the
project folder:

```bash
uv run python -c "import pandas; print(pandas.__version__)"
```

It should print `3.1.1`. In your editor, the interpreter button should show the
project environment rather than "Global"; if it still says "Global", the
project environment is not selected.

### 4. Render the report

From the project folder, run:

```bash
uv run quarto render analysis/mortality_in_heart_failure_patients.qmd
```

`uv run` runs Quarto inside the project environment, so you do not need to
activate `.venv` first. The report is saved as a single, self-contained file,
`analysis/mortality_in_heart_failure_patients.html`. Rendered output is
ignored by git, so it is not committed.

### Adding or removing packages

Use uv rather than pip, so the change is recorded for everyone:

```bash
uv add <package>          # a package the analysis uses
uv add --dev <package>    # a development tool, such as jupyter
uv remove <package>
```

Then commit `pyproject.toml` and `uv.lock` together. After pulling changes
from teammates, run `uv sync` again to update your environment.

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