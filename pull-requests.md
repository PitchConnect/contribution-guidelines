# Pull Request Process

This document outlines the process for creating, reviewing, and merging pull requests in PitchConnect projects.

## Table of Contents

- [Creating a Pull Request](#creating-a-pull-request)
- [PR Description Guidelines](#pr-description-guidelines)
- [Review Process](#review-process)
- [Addressing Feedback](#addressing-feedback)
- [Merge Guidelines](#merge-guidelines)
- [After Merging](#after-merging)

## Creating a Pull Request

1. **Ensure your branch is up to date**:
   ```bash
   git checkout develop
   git pull
   git checkout your-branch
   git rebase develop
   ```

2. **Run tests and linting locally**:
   ```bash
   # Run tests
   pytest
   
   # Run linting
   flake8
   mypy .
   ```

3. **Push your changes**:
   ```bash
   git push origin your-branch
   ```

4. **Create a PR through GitHub**:
   - Go to the repository on GitHub
   - Click "Pull requests" > "New pull request"
   - Select your branch and the target branch (usually `develop`)
   - Click "Create pull request"
   - Fill out the PR template completely

## PR Description Guidelines

A good PR description should include:

1. **What**: A clear explanation of what changes are being made
2. **Why**: The reason for the changes (reference issues with "Fixes #123")
3. **How**: A brief explanation of how the changes work
4. **Testing**: How the changes were tested
5. **Screenshots**: For UI changes (if applicable)
6. **Additional Notes**: Any other relevant information

Example:

```markdown
## Description
This PR adds user authentication via OAuth to simplify the login process.

## Related Issue
Fixes #42

## Changes Made
- Added OAuth client in `auth/oauth.py`
- Updated user model to store OAuth tokens
- Added login flow in the frontend
- Updated tests to cover OAuth scenarios

## How to Test
1. Configure OAuth credentials in `.env` (see README)
2. Run the server and navigate to /login
3. Click "Login with Google" and verify the flow works

## Screenshots
![Login Screen](https://example.com/screenshot.png)

## Additional Notes
This requires the new environment variables documented in the README.
```

## Review Process

1. **Automated Checks**:
   - Wait for CI/CD pipelines to complete
   - Address any failing tests or linting issues

2. **Request Reviews**:
   - Request reviews from at least one team member
   - For complex changes, request reviews from multiple team members

3. **Review Criteria**:
   - Code correctness and quality
   - Test coverage
   - Documentation
   - Security considerations
   - Performance implications

## Addressing Feedback

1. **Respond to all comments**:
   - Acknowledge feedback with a comment
   - Explain your reasoning if you disagree
   - Mark resolved when addressed

2. **Make requested changes**:
   ```bash
   git checkout your-branch
   # Make changes
   git add .
   git commit -m "Address review feedback"
   git push origin your-branch
   ```

3. **Request re-review**:
   - After addressing all feedback, request a re-review

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

## After Merging

1. **Delete the branch**:
   ```bash
   git branch -d your-branch
   git push origin --delete your-branch
   ```

2. **Verify issue closure**:
   - Check that any linked issues are properly closed
   - Add any follow-up comments to the issues if needed

3. **Update documentation**:
   - Update any relevant documentation
   - Notify team members of significant changes

4. **Monitor deployment**:
   - For changes that trigger deployments, monitor the deployment process
   - Verify the changes work in the deployed environment
