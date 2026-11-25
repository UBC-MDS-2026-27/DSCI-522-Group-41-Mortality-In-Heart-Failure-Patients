# Contributing to Heart Failure Mortality Prediction

Thank you for your interest in contributing to our project! Contributions that improve the analysis, code, documentation, or clarity of our findings are welcome.

## 1. Reporting Bugs and Suggesting Improvements

If you find an error, have a question, or would like to suggest an improvement:

1. Check whether an existing issue already covers it.
2. Open a new GitHub Issue.
3. Provide a clear description of the problem or suggestion.
4. Include relevant details, such as code, error messages, or screenshots, where appropriate.

## 2. Setting Up the Project

We develop and run our project inside a Docker container to ensure that everyone uses the same software and package versions.

Before contributing, follow the setup instructions in our [README.md](README.md). These instructions explain how to:

- Generate an SSH key.
- Download the project Docker image using `docker compose pull`.

All commands below should be run from the root directory of the repository unless otherwise specified.

## 3. Working in the Docker Container with Positron

We use Positron to edit and run our project inside the Docker container through SSH. This ensures that all contributors work in the same development environment.

### 3.1 Initial Setup (Once Before Your First Connection)

1. **Install Positron**

   Download and install [Positron](https://positron.posit.co/) on your computer. Its Remote SSH functionality is built in, so you do not need to install an additional extension.

2. **Check your Git identity**

   Open your computer's terminal and run:

   ```bash
   git config --global user.name
   git config --global user.email
   ```

   These commands should display your Git name and the email associated with your GitHub account.

   If they are not configured, set them using:

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

   The `docker-compose.yml` file shares your Git configuration with the container, allowing your commits inside the container to be associated with your GitHub identity.

3. **Complete the README setup**

   Ensure you have completed the SSH key setup and downloaded the Docker image as described in the [README.md](README.md).

### 3.2 Connecting to the Container Each Time You Work

1. Open a terminal on your computer and navigate to the root directory of the repository.

2. Start the Docker container in the background:

   ```bash
   docker compose up -d
   ```

3. Check that the container is running:

   ```bash
   docker compose ps
   ```

   The service `analysis-env` should appear as running.

4. Open Positron and launch the Command Palette:

   - Mac: `Cmd + Shift + P`
   - Windows: `Ctrl + Shift + P`

5. Search for and select **Remote SSH: Show Remote Menu**, then choose **Connect to Host**.

6. Enter the SSH connection address:

   ```text
   root@localhost:2222
   ```

   Press Enter.

   - If prompted to select the remote platform, choose Linux.
   - If asked whether you trust the host fingerprint, select Continue.
   - On the first connection, Positron will install its server inside the container. This may take a few minutes.

7. **Open the project directory**

   Once connected, Positron may display an empty Explorer and open the terminal in `/root`. This is normal.

   - Select Open Folder in the Explorer.
   - Enter the following directory:

     ```text
     /workspace
     ```

   - Confirm the selection.

   Your project files should now appear in the Explorer.

8. **Select the correct Python interpreter**

   Make sure Positron uses the Python environment created by `uv` inside the Docker container.

   - Click the interpreter selector in Positron.
   - Select New Console Session.
   - Choose the Python 3.x environment associated with `uv` and your project.
   - The interpreter path should be:

     ```text
     /opt/venv/bin/python
     ```

   If it does not appear:

   - Open the Command Palette.
   - Select Python: Select Interpreter.
   - Choose Enter interpreter path.
   - Enter `/opt/venv/bin/python`.

   **Important:** Do not select `/workspace/.venv`. That environment belongs to your local computer, not the Docker container.

   To verify the interpreter, run:

   ```python
   import sys
   print(sys.executable)
   ```

   The output should be:

   ```text
   /opt/venv/bin/python
   ```

9. You can now work on the project as usual. Your Positron terminal, Python console, and report rendering will run inside the Docker container.

10. **Stop the container when you finish working**

    Close the Positron remote window, then run this command in your computer's terminal:

    ```bash
    docker compose down
    ```

### 3.3 Troubleshooting SSH Connections

If Positron cannot connect to the Docker container, check the following:

- **SSH public key appears as a folder:** Run `docker compose down`, remove the incorrectly created `~/.ssh/id_ed25519.pub` folder, generate your SSH key as described in the README, and restart the container.

- **Git configuration appears as a folder:** Run `docker compose down`, remove the incorrectly created `~/.gitconfig` folder, configure your Git name and email, and restart the container.

- **SSH asks for a password:** Check that your public key is named `id_ed25519.pub` and that the path in `docker-compose.yml` is correct.

- **Remote host identification has changed:** Run:

  ```bash
  ssh-keygen -R "[localhost]:2222"
  ```

  Then reconnect to the container.

- **GitHub asks you to sign in when pushing:** Complete the GitHub authentication process in the browser window opened by Positron.

- **Port 2222 is already in use:** Change the port mapping in `docker-compose.yml` (for example, to `2223:22`) and connect using `root@localhost:2223`.

- **Linux SSH permission issue:** If SSH refuses the mounted key because of file ownership, uncomment the `StrictModes no` configuration line in the Dockerfile, commit and push the change, and use the newly published image.

## 4. Adding or Updating Packages

All Python dependencies are managed using `uv`. Contributors should not install project dependencies manually on their local computers.

When adding or updating a package:

1. Start from an up-to-date `main` branch.
2. Create a separate branch for the change:

   ```bash
   git switch main
   git pull origin main
   git switch -c add-package-name
   ```

3. Add the package using `uv`, specifying its exact version:

   ```bash
   uv add package-name==version
   ```

   This updates both `pyproject.toml` and `uv.lock`.

4. Commit and push the updated dependency files:

   ```bash
   git add pyproject.toml uv.lock
   git commit -m "Add package-name dependency"
   git push origin add-package-name
   ```

5. Wait for GitHub Actions to build and publish the updated Docker image to Docker Hub. The workflow will also update the image tag in `docker-compose.yml` on your branch.

6. Pull the latest changes and download the newly published image:

   ```bash
   git pull
   docker compose pull
   ```

7. Open a Pull Request from your branch into `main`.

8. After the Pull Request is reviewed and merged, wait for GitHub Actions to publish the image for the updated `main` branch.

9. Update your local `main` branch and download the latest image:

   ```bash
   git switch main
   git pull origin main
   docker compose pull
   ```

This ensures that all team members use the same updated dependencies and Docker environment.

## 5. Publishing the Report on GitHub Pages

Our project report is published through GitHub Pages so that readers can access the analysis without cloning the repository.

Whenever the report is updated:

1. Re-render the report inside the Docker container.

   For a Python project, run:

   ```bash
   docker compose run --rm analysis-env uv run quarto render
   ```

2. Ensure that the rendered HTML report is self-contained by enabling `embed-resources: true` in the Quarto HTML configuration.

3. Create the `docs` directory if it does not already exist:

   ```bash
   mkdir -p docs
   ```

4. Copy the newly rendered HTML report into `docs/index.html`:

   ```bash
   cp analysis/mortality_in_heart_failure_patients.html docs/index.html
   ```

   Replace the placeholder with the actual path to the rendered report.

5. Create the `.nojekyll` file:

   ```bash
   touch docs/.nojekyll
   ```

6. Commit and push the updated report:

   ```bash
   git add docs/
   git commit -m "Update published project report"
   git push
   ```

7. Ensure that GitHub Pages is configured to deploy from the `main` branch and the `/docs` folder under the repository's Settings > Pages.

8. Verify that the published report is accessible and that all figures and visualizations display correctly.

**Important:** Every time the report is re-rendered, copy the latest HTML file into `docs/index.html` and push the changes so that the published report remains up to date.

## 6. Making Changes and Submitting Pull Requests

To maintain an organized and collaborative workflow:

1. Always work on a separate branch rather than committing directly to `main`.
2. Pull the latest changes from `main` before creating a new branch.
3. Keep each branch focused on one specific task or improvement.
4. Test your changes before committing.
5. Use clear and descriptive commit messages.
6. Push your branch to GitHub and open a Pull Request into `main`.
7. Describe what you changed and why.
8. Link the relevant issue, if applicable.
9. Request a review from another team member.
10. Address feedback before merging.

At least one other team member must review and approve a Pull Request before it is merged. Contributors should not merge their own Pull Requests without the required review.

## 7. Code, Data and Analysis Guidelines

To maintain consistency and reproducibility:

- Write clear, readable, and understandable code.
- Use descriptive names for variables and functions.
- Follow the existing project structure and coding style.
- Avoid unnecessary changes unrelated to the task.
- Include comments when they help explain complex code.
- Update documentation when changes affect the project workflow or analysis.
- Use the project's existing dataset and documented data-processing workflow unless a change is discussed with the team.
- Avoid using the test set to make decisions about model selection or feature engineering.
- Ensure that visualizations and reported results accurately represent the data.
- Explain analytical decisions clearly and avoid unsupported conclusions.
- Preserve reproducibility by documenting changes to the analysis and dependencies.

## 8. AI Usage Policy

Generative AI tools, including ChatGPT, GitHub Copilot, and Claude, may be used to assist contributors with understanding code, debugging, brainstorming, improving documentation, and explaining statistical or machine-learning concepts.

When AI tools are used:

- Contributors must disclose their AI usage in their issue or Pull Request, including the tool used and how it assisted.
- AI-generated code, explanations, and documentation must be reviewed, tested, and verified before submission.
- Contributors must understand the work they submit and be able to explain their implementation and decisions.
- AI tools must not independently create, submit, review, approve, or merge Pull Requests or issues on behalf of contributors.
- Contributors remain responsible for the accuracy, originality, quality, and integrity of their contributions.
- Do not submit sensitive, confidential, or private information to AI tools.

AI tools may assist with the contribution process, but all issues and Pull Requests must be opened, reviewed, and merged by human contributors in accordance with course expectations.

## 9. Questions

If you have questions about contributing, open a GitHub Issue and clearly describe what you need help with. A member of the project team can respond and help clarify the workflow.

Thank you for helping improve our project!