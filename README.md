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

The analysis runs inside a Docker container, so you do not need to install
Python, uv or Quarto yourself. These steps work on both macOS and Windows.

### 1. Install Docker and clone the repository

Install [Docker Desktop](https://www.docker.com/products/docker-desktop/) and
make sure it is running. Then clone this repository and move into its folder:

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-41-Mortality-In-Heart-Failure-Patients.git
cd DSCI-522-Group-41-Mortality-In-Heart-Failure-Patients
```

### 2. Create an ssh key

The container expects an ssh public key at `~/.ssh/id_ed25519.pub`. Check
whether you already have one by running `ls ~/.ssh/id_ed25519.pub`. If the file
is not found, create a key with the command below and press Enter at every
prompt to accept the defaults:

```bash
ssh-keygen -t ed25519
```

If you skip this step, Docker creates a folder named `id_ed25519.pub` in
place of the file and the container will not start correctly.

### 3. Download the container image

From the project folder, download the image listed in `docker-compose.yml`:

```bash
docker compose pull
```

The image is about 1.5 GB, so the first download can take a few minutes.

### 4. Render the report

From the project folder, run:

```bash
docker compose run --rm analysis-env uv run quarto render analysis/mortality_in_heart_failure_patients.qmd
```

This command starts the container, renders the report inside it and saves the
result to `analysis/mortality_in_heart_failure_patients.html` in your project
folder.

### 5. Stopping the container

The `--rm` flag in the command above removes the container as soon as the
report finishes rendering, so there is nothing left to stop. If you instead
started the container in the background with `docker compose up -d`, stop it
with `docker compose down` when you are done.

If you want to change the analysis or work inside the container, see
[CONTRIBUTING.md](CONTRIBUTING.md).

## Dependencies

The analysis runs in a Docker image published on
[Docker Hub](https://hub.docker.com/r/itsluismario/dsci-522-group-41-mortality-in-heart-failure-patients),
which contains Python, uv, Quarto and every package the project uses. The
Python packages and their versions are pinned in [`pyproject.toml`](pyproject.toml)
and [`uv.lock`](uv.lock).

## Licenses

The code in this repository is licensed under the MIT License, and the report
is licensed under the Creative Commons Attribution-NonCommercial-NoDerivatives
4.0 International License (CC BY-NC-ND 4.0). See [`LICENSE.md`](LICENSE.md)
for the full text.

## Use of generative AI

We used Claude to help draft the structure of this README. All AI suggestions
were reviewed, edited and approved by team members, who remain responsible for
the final content. 