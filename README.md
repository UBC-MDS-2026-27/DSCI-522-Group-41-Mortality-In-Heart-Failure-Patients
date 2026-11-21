# Predicting Mortality in Heart Failure Patients from Clinical Records

**Authors:** Linda Arthur, Luis Mario, Yunpeng Xie

**Rendered report:** [View the report](https://ubc-mds-2026-27.github.io/DSCI-522-Group-41-Mortality-In-Heart-Failure-Patients/analysis/mortality_in_heart_failure_patients.html)

## Summary

In this project, we ask whether we can predict if a patient with heart failure
will die during the follow-up period from routinely collected clinical
measurements, such as age, ejection fraction, serum creatinine, serum sodium,
blood pressure and anaemia. We use the
[Heart Failure Clinical Records data set](https://archive.ics.uci.edu/dataset/519/heart+failure+clinical+records)
from the UCI Machine Learning Repository, which contains the medical records
of 299 patients with advanced heart failure (NYHA class III or IV) treated at a
hospital in Faisalabad, Pakistan, in 2015. Of these patients, 96 (about 32%)
died during follow-up. We exclude follow-up time as a predictor because it is
directly linked to the outcome and would leak information about the target.
A model like this could help clinicians identify the patients at greatest risk
so they can be prioritized for closer follow-up and treatment.

We trained a logistic regression model and compared it with a baseline model
that always predicts survival. On the held-out test set, our model achieved an
accuracy of 73.3% and a recall of 42.1%, correctly identifying 8 of the 19
patients who died. Although it performs better than the baseline, it misses
most patients who died, so it is not reliable enough to guide clinical
decisions on its own. Because the data come from 299 patients with advanced
disease at a single hospital, our results may not generalize to patients with
milder heart failure or to other populations.

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
not recorded for the rest of the team. Use `uv add <package>` instead.

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
`analysis/mortality_in_heart_failure_patients.html`.

To preview the report while you work on it in Positron, open
`analysis/mortality_in_heart_failure_patients.qmd` and either click the
**Preview** button at the top of the editor, or open the Command Palette
(**Cmd + Shift + P** on macOS, **Ctrl + Shift + P** on Windows) and run
**Quarto: Preview** (shortcut **Cmd + Shift + K** / **Ctrl + Shift + K**). The
preview opens in Positron's Viewer pane and updates each time you save. Select
the project environment first (step 3), or the code chunks will run with the
wrong Python.

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