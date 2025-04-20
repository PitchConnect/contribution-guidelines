# GitFlow Workflow Guide

This document provides detailed instructions for following the GitFlow workflow in PitchConnect projects.

## Table of Contents

- [Branch Structure](#branch-structure)
- [Workflow Overview](#workflow-overview)
- [Detailed Workflow Steps](#detailed-workflow-steps)
  - [Feature Development](#feature-development)
  - [Bug Fixes](#bug-fixes)
  - [Release Process](#release-process)
  - [Hotfixes](#hotfixes)
- [Merge Guidelines](#merge-guidelines)
- [Branch Cleanup](#branch-cleanup)
- [Commit Message Guidelines](#commit-message-guidelines)

## Branch Structure

- `main`: Production-ready code. Always stable and releasable.
- `develop`: Integration branch for features. Contains code for the next release.
- `feature/*`: Feature branches for new functionality.
- `bugfix/*`: Bug fix branches for issues.
- `release/*`: Release preparation branches.
- `hotfix/*`: Emergency fixes for production issues.

## Workflow Overview

The GitFlow workflow is designed around project releases and provides a robust framework for managing larger projects. Here's a high-level overview:

1. A `develop` branch is created from `main`
2. Feature branches are created from `develop`
3. When a feature is complete, it's merged into `develop`
4. When `develop` has enough features for a release, a `release` branch is created
5. After the release is finalized, it's merged into `main` and tagged with a version
6. If an issue in `main` needs immediate fixing, a `hotfix` branch is created
7. The hotfix is merged into both `main` and `develop`

## Detailed Workflow Steps

### Feature Development

1. **Create a feature branch from `develop`**:
   ```bash
   git checkout develop
   git pull
   git checkout -b feature/your-feature-name
   ```

2. **Make your changes**:
   - Implement your feature
   - Commit frequently with clear messages
   - Push your branch to GitHub
   ```bash
   git add .
   git commit -m "Add feature: your feature description"
   git push origin feature/your-feature-name
   ```

3. **Create a Pull Request**:
   - Create a PR from your feature branch to `develop`
   - Reference any related issues
   - Request reviews
   - Ensure CI/CD checks pass

4. **Review and Merge**:
   - Address review feedback
   - Once approved, your changes will be squash-merged into `develop`
   - Delete the feature branch after merging

### Bug Fixes

1. **Create a bugfix branch from `develop`**:
   ```bash
   git checkout develop
   git pull
   git checkout -b bugfix/issue-description
   ```

2. **Fix the bug**:
   - Implement your fix
   - Add tests to prevent regression
   - Commit with a clear message
   ```bash
   git add .
   git commit -m "Fix: description of the bug fix"
   git push origin bugfix/issue-description
   ```

3. **Create a Pull Request**:
   - Create a PR from your bugfix branch to `develop`
   - Reference the issue being fixed (e.g., "Fixes #123")
   - Request reviews
   - Ensure CI/CD checks pass

4. **Review and Merge**:
   - Address review feedback
   - Once approved, your changes will be squash-merged into `develop`
   - Delete the bugfix branch after merging

### Release Process

1. **Create a release branch from `develop`**:
   ```bash
   git checkout develop
   git pull
   git checkout -b release/1.0.0
   ```

2. **Prepare the release**:
   - Update version numbers
   - Update CHANGELOG.md
   - Make any final adjustments
   - Commit these changes
   ```bash
   git add .
   git commit -m "Prepare release 1.0.0"
   git push origin release/1.0.0
   ```

3. **Create a Pull Request to `main`**:
   - Create a PR from your release branch to `main`
   - Provide a summary of the release
   - Request reviews
   - Ensure CI/CD checks pass

4. **Merge and Tag**:
   - Once approved, merge the release branch into `main` (no squash)
   - Tag the release on `main`
   ```bash
   git checkout main
   git pull
   git tag -a v1.0.0 -m "Version 1.0.0"
   git push origin v1.0.0
   ```

5. **Merge back to `develop`**:
   - Merge the release branch back to `develop`
   ```bash
   git checkout develop
   git pull
   git merge --no-ff release/1.0.0
   git push origin develop
   ```

6. **Clean up**:
   - Delete the release branch
   ```bash
   git branch -d release/1.0.0
   git push origin --delete release/1.0.0
   ```

### Hotfixes

1. **Create a hotfix branch from `main`**:
   ```bash
   git checkout main
   git pull
   git checkout -b hotfix/critical-issue
   ```

2. **Fix the issue**:
   - Implement your fix
   - Update version number (patch increment)
   - Add tests to prevent regression
   - Commit with a clear message
   ```bash
   git add .
   git commit -m "Hotfix: description of the critical fix"
   git push origin hotfix/critical-issue
   ```

3. **Create a Pull Request to `main`**:
   - Create a PR from your hotfix branch to `main`
   - Reference the issue being fixed
   - Request reviews
   - Ensure CI/CD checks pass

4. **Merge and Tag**:
   - Once approved, merge the hotfix branch into `main` (no squash)
   - Tag the hotfix on `main`
   ```bash
   git checkout main
   git pull
   git tag -a v1.0.1 -m "Hotfix 1.0.1"
   git push origin v1.0.1
   ```

5. **Merge to `develop`**:
   - Merge the hotfix branch to `develop` as well
   ```bash
   git checkout develop
   git pull
   git merge --no-ff hotfix/critical-issue
   git push origin develop
   ```

6. **Clean up**:
   - Delete the hotfix branch
   ```bash
   git branch -d hotfix/critical-issue
   git push origin --delete hotfix/critical-issue
   ```

## Merge Guidelines

When merging Pull Requests, follow these guidelines to maintain a clean and meaningful history:

### When to use Squash Merge

- For feature branches with multiple small, incremental commits
- When commit messages in the branch are not particularly meaningful
- For simple changes where the commit history isn't important
- For most documentation changes

### When to use Regular Merge (--no-ff)

- For larger features with a well-structured commit history
- When the individual commits tell a story about how the feature was developed
- When each commit represents a logical, atomic change
- For complex refactorings where the step-by-step changes are important
- Always for release and hotfix branches

### After Merging

- Always delete the feature branch both locally and remotely
- Verify that the issue is properly closed if the PR resolves an issue
- Check if any documentation needs to be updated

## Branch Cleanup

### After Merging

- Always delete branches after merging
- Use `git branch -d branch-name` for local branch deletion
- Use `git push origin --delete branch-name` for remote branch deletion

### Stale Branches

- Periodically review and clean up old branches
- Consider deleting branches that haven't been updated in 3+ months
- Before deleting, check if the branch contains unique work
- If a branch contains valuable work, create an issue to track it

### Abandoned PRs

- If a PR is abandoned, comment asking for status
- After 2 weeks without response, consider closing the PR
- Mention that the work can be continued in a new PR if needed

## Commit Message Guidelines

- Use the format: `Type: Short description`
- Types: `Fix`, `Feature`, `Docs`, `Style`, `Refactor`, `Test`, `Chore`
- Example: `Fix: Ensure proper error handling in authentication flow`
- Keep messages clear, concise, and descriptive
- Reference issue numbers when applicable: `Fix #123: Add error handling`

### Good Commit Message Examples

```
Feature: Add user authentication via OAuth
Fix #42: Resolve race condition in data processing
Docs: Update installation instructions for Windows
Refactor: Simplify error handling in API client
Test: Add integration tests for payment processing
```

### Poor Commit Message Examples

```
Fixed stuff
Updated code
WIP
Changes
```

By following these guidelines, we can maintain a clean, organized repository with a clear history of changes.
