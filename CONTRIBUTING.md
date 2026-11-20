# Contributing to Heart Failure Mortality Prediction

Thank you for your interest in contributing to our project! Contributions that improve the analysis, code, documentation, or clarity of our findings are welcome.

## 1. Reporting Bugs and Suggesting Improvements

If you find an error, have a question, or would like to suggest an improvement:

1. Check whether an existing issue already covers it.
2. Open a new GitHub Issue.
3. Provide a clear description of the problem or suggestion.
4. Include relevant details, such as code, error messages, or screenshots, where appropriate.

## 2. Making Changes

Please work on a separate branch rather than making changes directly to `main`.

1. Pull the latest changes from `main`.
2. Create a new branch for your work.
3. Make your changes.
4. Test your changes and ensure they work as expected.
5. Commit your changes with a clear commit message.
6. Push your branch to GitHub.

Example:

```bash
git switch main
git pull origin main
git switch -c feature/your-feature-name
```

After making your changes:

```bash
git add .
git commit -m "Describe your changes"
git push origin feature/your-feature-name
```

## 3. Submitting Changes

When your changes are ready:

1. Open a Pull Request (PR) from your branch into `main`.
2. Describe what you changed and why.
3. Link the relevant issue, if applicable.
4. Request a review from a team member.
5. Address any feedback before the PR is merged.

Pull requests must be reviewed and merged by project team members. Contributors should not merge their own pull requests without the required review.

## 4. Code and Documentation Guidelines

To maintain consistency throughout the project:

- Write clear, readable, and understandable code.
- Use descriptive names for variables and functions.
- Follow the existing project structure and coding style.
- Avoid unnecessary changes unrelated to the task.
- Include comments when they help explain complex code.
- Update documentation when your changes affect the project workflow or analysis.
- Ensure your changes do not introduce errors or unintended modifications to the analysis.

## 5. Data and Analysis Guidelines

Contributions to the analysis should:

- Use the project's existing dataset and documented data-processing workflow unless a change is discussed with the team.
- Avoid using the test set to make decisions about model selection or feature engineering.
- Ensure that visualizations and reported results accurately represent the data.
- Explain analytical decisions clearly and avoid unsupported conclusions.
- Preserve reproducibility by documenting changes to the analysis or dependencies.

## 6. AI Usage Policy

Generative AI tools, including ChatGPT, GitHub Copilot, and Claude, may be used to assist contributors with tasks such as understanding code, debugging, brainstorming, improving documentation, and explaining statistical or machine-learning concepts.

When AI tools are used:

- Contributors must disclose their AI usage in their issue or pull request, including the tool used and how it assisted.
- AI-generated code, explanations, and documentation must be reviewed, tested, and verified by the contributor before submission.
- Contributors must understand the work they submit and be able to explain their implementation and decisions.
- AI tools must not be used to independently create, submit, review, approve, or merge pull requests or issues on behalf of contributors.
- Contributors remain responsible for the accuracy, originality, quality, and integrity of their contributions.
- Do not submit sensitive, confidential, or private information to AI tools.

AI tools may assist with the contribution process, but all issues and pull requests must be opened, reviewed, and merged by human contributors in accordance with course expectations.

## 7. Questions

If you have questions about contributing, open a GitHub Issue and clearly describe what you need help with. A member of the project team can respond and help clarify the workflow.

Thank you for helping improve our project!
