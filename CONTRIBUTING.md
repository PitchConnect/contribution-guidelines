# Contributing to PitchConnect Projects

<!-- START COMMON SECTION v1.0 (Last updated: 2023-05-02) -->

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
  - [Branching Model](#branching-model)
  - [Feature Development](#feature-development)
  - [Bug Fixes](#bug-fixes)
  - [Releases](#releases)
  - [Hotfixes](#hotfixes)
- [Pull Request Process](#pull-request-process)
  - [Creating a Pull Request](#creating-a-pull-request)
  - [PR Review Process](#pr-review-process)
  - [Merging Guidelines](#merging-guidelines)
- [Coding Standards](#coding-standards)
  - [General Guidelines](#general-guidelines)
  - [Language-Specific Guidelines](#language-specific-guidelines)
  - [Documentation](#documentation)
  - [Testing](#testing)
- [Working with AI Assistants](#working-with-ai-assistants)
  - [When to Use AI Assistance](#when-to-use-ai-assistance)
  - [Best Practices](#best-practices)
  - [GitHub CLI Usage](#github-cli-usage)
- [Issue Lifecycle and Automation](#issue-lifecycle-and-automation)
  - [Issue Status Automation](#issue-status-automation)
  - [Referencing Issues in PRs](#referencing-issues-in-prs)
  - [Manual Issue Closure](#manual-issue-closure)
- [Work in Progress](#work-in-progress)
- [Repository-Specific Guidelines](#repository-specific-guidelines)

## Code of Conduct

This project and everyone participating in it is governed by the [PitchConnect Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to the repository maintainers.

## Getting Started

To get started contributing to this project:

1. Fork the repository
2. Clone your fork: `gh repo clone your-username/repo-name`
3. Create a feature branch: `git checkout -b feature/your-feature-name`
4. Install dependencies according to the project's README
5. Make your changes
6. Run tests to ensure your changes don't break existing functionality
7. Commit your changes with descriptive commit messages
8. Push to your branch: `git push origin feature/your-feature-name`
9. Create a Pull Request

## Development Workflow

<a id="branching-model"></a>
### Branching Model

This project follows the GitFlow workflow:

- `main`: Production-ready code
- `develop`: Latest development changes
- `feature/*`: New features
- `bugfix/*`: Bug fixes
- `release/*`: Release preparation
- `hotfix/*`: Urgent fixes for production

<a id="feature-development"></a>
### Feature Development

1. Create a feature branch from `develop`:
   ```bash
   git checkout develop
   git pull
   git checkout -b feature/your-feature-name
   ```

2. Implement your changes, committing regularly with descriptive messages
3. Push your branch to GitHub:
   ```bash
   git push -u origin feature/your-feature-name
   ```

4. Create a Pull Request to merge into `develop`
5. Address review feedback
6. Once approved, merge into `develop`

<a id="bug-fixes"></a>
### Bug Fixes

1. Create a bugfix branch from `develop`:
   ```bash
   git checkout develop
   git pull
   git checkout -b bugfix/bug-description
   ```

2. Fix the bug, adding tests to prevent regression
3. Push your branch to GitHub:
   ```bash
   git push -u origin bugfix/bug-description
   ```

4. Create a Pull Request to merge into `develop`
5. Once approved, merge into `develop`

<a id="releases"></a>
### Releases

1. Create a release branch from `develop`:
   ```bash
   git checkout develop
   git pull
   git checkout -b release/v1.2.3
   ```

2. Make any final adjustments and version bumps
3. Create a Pull Request to merge into `main`
4. Once approved, merge into `main`
5. Tag the release:
   ```bash
   git checkout main
   git pull
   git tag -a v1.2.3 -m "Release v1.2.3"
   git push origin v1.2.3
   ```

6. Merge `main` back into `develop`:
   ```bash
   git checkout develop
   git merge main
   git push
   ```

<a id="hotfixes"></a>
### Hotfixes

1. Create a hotfix branch from `main`:
   ```bash
   git checkout main
   git pull
   git checkout -b hotfix/critical-bug-fix
   ```

2. Fix the critical bug
3. Create a Pull Request to merge into `main`
4. Once approved, merge into `main`
5. Tag the hotfix:
   ```bash
   git checkout main
   git pull
   git tag -a v1.2.4 -m "Hotfix v1.2.4"
   git push origin v1.2.4
   ```

6. Merge `main` back into `develop`:
   ```bash
   git checkout develop
   git merge main
   git push
   ```

## Pull Request Process

<a id="creating-a-pull-request"></a>
### Creating a Pull Request

1. Ensure your code passes all tests and linting
2. Update documentation to reflect any changes
3. Create a Pull Request with a clear title and description
4. Reference any related issues using keywords like "Fixes #123"
5. Add appropriate labels
6. Request reviews from relevant team members

<a id="pr-review-process"></a>
### PR Review Process

1. Reviewers will check for:
   - Code quality and correctness
   - Test coverage
   - Documentation
   - Adherence to coding standards
   - Potential side effects

2. Address all review comments
3. Once approved, the PR can be merged

<a id="merging-guidelines"></a>
### Merging Guidelines

- Feature and bugfix branches should be merged into `develop` using squash merge
- Release branches should be merged into `main` using a regular merge (no squash)
- Hotfix branches should be merged into both `main` and `develop` using a regular merge

## Coding Standards

<a id="general-guidelines"></a>
### General Guidelines

- Write clean, readable, and maintainable code
- Follow the principle of "Don't Repeat Yourself" (DRY)
- Keep functions and methods small and focused
- Use meaningful variable and function names
- Add comments for complex logic, but prefer self-documenting code
- Follow the project's existing code style

<a id="language-specific-guidelines"></a>
### Language-Specific Guidelines

#### Python
- Follow PEP 8 style guide
- Use type hints where appropriate
- Use docstrings for functions and classes
- Use virtual environments for dependency management

#### JavaScript/TypeScript
- Follow ESLint configuration
- Use modern ES6+ features
- Prefer async/await over callbacks
- Use TypeScript types/interfaces

#### Other Languages
- Follow the established conventions for the language
- Consult language-specific style guides

<a id="documentation"></a>
### Documentation

- Keep README.md up to date
- Document public APIs
- Include examples where helpful
- Update documentation when making changes
- Use clear and concise language

<a id="testing"></a>
### Testing

- Write unit tests for new functionality
- Ensure existing tests pass
- Aim for high test coverage
- Include integration tests where appropriate
- Test edge cases and error conditions

## Working with AI Assistants

<a id="when-to-use-ai-assistance"></a>
### When to Use AI Assistance

AI assistants can be helpful for:
- Generating boilerplate code
- Explaining complex code
- Debugging issues
- Writing tests
- Documenting code
- Suggesting refactoring approaches

<a id="best-practices"></a>
### Best Practices

When working with AI assistants:

1. **Review all generated code** thoroughly before committing
2. **Understand the code** before using it
3. **Test generated code** rigorously
4. **Provide clear instructions** to get better results
5. **Break down complex tasks** into smaller chunks
6. **Check for security issues** in generated code
7. **Verify licensing compatibility** of suggested solutions
8. **Read all comments** on issues and PRs, not just the initial description

<a id="github-cli-usage"></a>
### GitHub CLI Usage

AI agents should use GitHub CLI (gh) for GitHub operations whenever possible. This provides a consistent interface and reduces the need for web browser interactions.

#### Common Commands

- Clone a repository: `gh repo clone PitchConnect/repo-name`
- Create an issue: `gh issue create --title "Issue title" --body-file issue.md`
- Create a PR: `gh pr create --title "PR title" --body-file pr.md`
- Check PR status: `gh pr status`
- Review a PR: `gh pr checkout {pr-number}`
- List issues: `gh issue list --state open`

#### Best Practices

- Always clean up temporary files after use
- Use `--body-file` instead of inline content for complex markdown
- Reference issues in PRs using the appropriate syntax

## Issue Lifecycle and Automation

<a id="issue-status-automation"></a>
### Issue Status Automation

This project uses automation to track issue status through the development lifecycle:

1. **When you create a Draft PR**:
   - Referenced issues will automatically be labeled as `in-progress`
   - A comment will be added to the issue linking to your PR

2. **When you mark a PR as Ready for Review**:
   - The `in-progress` label will be removed
   - Issues will be labeled as `review-ready`

3. **When your PR is merged to `develop`**:
   - Issues will be labeled as `merged-to-develop`
   - Issues will NOT be closed automatically at this stage
   - DO NOT manually close issues when merging to develop

4. **When a release is created**:
   - All `merged-to-develop` issues will be automatically included in the release PR
   - When the release is merged to `main`, issues will be automatically closed
   - Issues will receive a `released` label

<a id="referencing-issues-in-prs"></a>
### Referencing Issues in PRs

Always reference issues in your PR using one of these keywords:
- `Fixes #123`
- `Resolves #123`
- `Closes #123`

Example PR description:
```
This PR adds user authentication via OAuth.

Fixes #123
```

This ensures the automation can properly track which issues are addressed by your PR.

<a id="manual-issue-closure"></a>
### Manual Issue Closure

Do not manually close issues when merging to develop. Issues should remain open until they are released to production (merged to main).

If you need to close an issue without a PR (e.g., duplicate, won't fix), add a comment explaining why.

## Work in Progress

When your work is not yet ready for review:

1. Create a **Draft Pull Request** instead of a regular PR
   - Use the dropdown menu next to "Create Pull Request" to select "Create Draft Pull Request"
   - This clearly indicates your PR is a work in progress
   - The PR cannot be merged until you mark it as ready for review

2. **IMPORTANT**: Do not mark a PR as ready for review until:
   - All CI/CD checks are passing
   - All pre-commit hooks have been run successfully
   - You have addressed any automated feedback
   - The code is fully ready for human review

3. When your work is complete and all checks pass:
   - Click "Ready for Review" to convert the Draft PR to a regular PR
   - This signals to reviewers that your work is ready for their attention

### CI/CD Pipeline Failures

If your PR fails CI/CD checks:

1. Review the failure logs carefully
2. Fix the issues in your branch
3. Push the changes to update the PR
4. Verify that all checks pass before marking as ready for review
5. If the CI/CD caught issues that should have been caught by pre-commit hooks, update the pre-commit configuration as well

Draft PRs are preferred over other methods like "WIP" in titles or special branches, as they provide a standard, built-in way to indicate work in progress.

## Repository-Specific Guidelines

Please refer to the repository-specific section below for any additional guidelines specific to this project.

<!-- END COMMON SECTION -->

## Repository-Specific Guidelines

This section contains guidelines specific to the contribution-guidelines repository.

### Purpose of This Repository

This repository serves as the central source of truth for contribution guidelines across all PitchConnect repositories. It contains:

1. The consolidated CONTRIBUTING.md file (this file)
2. Templates for repository-specific CONTRIBUTING.md files
3. Issue and PR templates
4. Other contribution-related documentation

### Updating Guidelines

When updating the contribution guidelines:

1. Make changes to the consolidated CONTRIBUTING.md file
2. Update any related templates or documentation
3. Create a PR to merge your changes
4. Once approved and merged, the changes will be propagated to other repositories

### Testing Changes

Before submitting a PR:

1. Preview the markdown to ensure proper formatting
2. Check that all links work correctly
3. Verify that the content is clear and consistent

### Special Considerations

Since these guidelines are used across multiple repositories:

1. Keep the language repository-agnostic where possible
2. Use clear section markers for the common content
3. Provide flexibility for repository-specific customizations
