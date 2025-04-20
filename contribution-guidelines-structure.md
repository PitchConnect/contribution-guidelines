# PitchConnect Contribution Guidelines Repository Structure

This document outlines the proposed structure for a centralized contribution guidelines repository.

## Repository Structure

```
contribution-guidelines/
├── README.md                     # Overview and navigation
├── CODE_OF_CONDUCT.md            # Organization-wide code of conduct
├── CONTRIBUTING.md               # Meta-contributing guide (how to contribute to these guidelines)
├── _config.yml                   # GitHub Pages configuration
├── index.md                      # Main page for GitHub Pages
├── workflow.md                   # Detailed GitFlow workflow guide
├── coding-standards.md           # Comprehensive coding standards
├── pull-requests.md              # Pull request process and best practices
├── testing.md                    # Testing guidelines and best practices
├── documentation.md              # Documentation standards
├── ai-guidelines.md              # Guidelines for AI usage and AI assistants
├── security.md                   # Security best practices
├── templates/                    # Templates directory
│   ├── CONTRIBUTING.md           # Template for project CONTRIBUTING.md
│   ├── pull_request_template.md  # PR template
│   ├── issue_templates/          # Issue templates
│   │   ├── bug_report.md         # Bug report template
│   │   ├── feature_request.md    # Feature request template
│   │   └── question.md           # Question template
│   └── workflows/                # GitHub Actions workflow templates
│       ├── python-tests.yml      # Python testing workflow
│       └── release.yml           # Release workflow
└── assets/                       # Assets for documentation
    ├── images/                   # Images for documentation
    │   ├── gitflow-diagram.png   # GitFlow workflow diagram
    │   └── pr-process.png        # PR process diagram
    └── css/                      # Custom CSS for GitHub Pages
        └── style.css             # Custom styles
```

## Key Files Content Overview

### README.md

The main README should provide an overview of the repository and how to navigate it:

```markdown
# PitchConnect Contribution Guidelines

This repository contains the centralized contribution guidelines for all PitchConnect projects.

## Purpose

These guidelines ensure consistency across all PitchConnect repositories and make it easier for contributors to work on multiple projects within the organization.

## How to Use These Guidelines

1. **For Project Maintainers**: Use the templates in the `templates/` directory for your project's contribution documentation.
2. **For Contributors**: Read the relevant guidelines before contributing to any PitchConnect project.
3. **For Everyone**: Suggest improvements to these guidelines by opening an issue or pull request.

## Documentation Website

These guidelines are also available as a website at [https://pitchconnect.github.io/contribution-guidelines](https://pitchconnect.github.io/contribution-guidelines).

## Table of Contents

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Workflow Guide](workflow.md)
- [Coding Standards](coding-standards.md)
- [Pull Request Process](pull-requests.md)
- [Testing Guidelines](testing.md)
- [Documentation Standards](documentation.md)
- [AI Contribution Guidelines](ai-guidelines.md)
- [Security Best Practices](security.md)
- [Templates](templates/)
```

### workflow.md

This file would contain detailed GitFlow workflow instructions:

```markdown
# GitFlow Workflow Guide

This document provides detailed instructions for following the GitFlow workflow in PitchConnect projects.

## Branch Structure

- `main`: Production-ready code. Always stable and releasable.
- `develop`: Integration branch for features. Contains code for the next release.
- `feature/*`: Feature branches for new functionality.
- `bugfix/*`: Bug fix branches for issues.
- `release/*`: Release preparation branches.
- `hotfix/*`: Emergency fixes for production issues.

## Workflow Diagram

![GitFlow Workflow Diagram](assets/images/gitflow-diagram.png)

## Detailed Workflow Steps

### Feature Development

1. **Create a feature branch from `develop`**:
   ```bash
   git checkout develop
   git pull
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes**:
   - Commit frequently with clear messages
   - Push your branch to GitHub

3. **Create a Pull Request**:
   - Create a PR from your feature branch to `develop`
   - Reference any related issues
   - Request reviews

4. **Review and Merge**:
   - Address review feedback
   - Once approved, your changes will be squash-merged into `develop`
   - Delete the feature branch after merging

[... and so on with detailed instructions for releases, hotfixes, etc. ...]
```

### ai-guidelines.md

This file would contain comprehensive guidelines for AI usage:

```markdown
# AI Contribution Guidelines

This document provides guidelines for using AI tools in development and for AI assistants contributing to PitchConnect projects.

## For Human Contributors Using AI

When using AI tools like GitHub Copilot, ChatGPT, or similar:

1. **Review all AI-generated code thoroughly**:
   - Ensure it follows our coding standards
   - Verify it works as expected
   - Check for security issues
   - Test it properly

2. **Disclose AI usage**:
   - Mention in your PR description if significant portions were AI-assisted
   - This helps reviewers focus on potential AI-specific issues

3. **Don't blindly trust AI output**:
   - AI can generate plausible-looking but incorrect code
   - AI may not understand project-specific constraints
   - AI might suggest outdated or insecure practices

[... more guidelines ...]

## For AI Assistants

If you are an AI assistant helping with PitchConnect projects:

1. **First Steps for AI Assistants**:
   - Read the CONTRIBUTING.md file for the specific project
   - Understand the codebase using tools like `codebase-retrieval`
   - Follow project conventions by observing existing patterns
   - Plan before coding by creating a detailed plan
   - Verify your understanding with the user

2. **Issue and Branch Management**:
   - Always reference issues in PRs using keywords like "Fixes #123"
   - When replacing a PR with another one, reference both the issue and the PR being replaced
   - Close issues automatically through PR merges when possible
   - Delete branches after merging to keep the repository clean

[... more guidelines ...]
```

## Implementation Plan

1. **Create the centralized repository**:
   - Create a new repository named `contribution-guidelines` in the PitchConnect organization
   - Set up the basic structure as outlined above

2. **Develop core content**:
   - Start with the most important files: workflow.md, coding-standards.md, and ai-guidelines.md
   - Use the best content from your existing CONTRIBUTING.md files

3. **Set up GitHub Pages**:
   - Configure GitHub Pages to serve the documentation
   - Add a simple theme and navigation

4. **Update project repositories**:
   - Replace existing CONTRIBUTING.md files with the new template
   - Customize the project-specific sections for each repository

5. **Add missing CONTRIBUTING.md files**:
   - Create new CONTRIBUTING.md files for repositories that don't have them

Would you like me to start creating any of these detailed guideline files for the centralized repository?
