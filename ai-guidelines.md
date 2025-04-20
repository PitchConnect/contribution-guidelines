# AI Contribution Guidelines

This document provides comprehensive guidelines for using AI tools in development and for AI assistants contributing to PitchConnect projects.

## Table of Contents

- [For Human Contributors Using AI](#for-human-contributors-using-ai)
- [For AI Assistants](#for-ai-assistants)
  - [First Steps for AI Assistants](#first-steps-for-ai-assistants)
  - [Working on Issues](#working-on-issues)
  - [Code Quality and Testing](#code-quality-and-testing)
  - [Communication](#communication)
  - [GitHub CLI Usage](#github-cli-usage)
  - [PR Descriptions](#pr-descriptions)
  - [Security Considerations](#security-considerations)

## For Human Contributors Using AI

When using AI tools like GitHub Copilot, ChatGPT, or similar:

### Review All AI-Generated Code Thoroughly

- Ensure it follows our coding standards
- Verify it works as expected
- Check for security issues
- Test it properly

### Disclose AI Usage

- Mention in your PR description if significant portions were AI-assisted
- This helps reviewers focus on potential AI-specific issues

### Don't Blindly Trust AI Output

- AI can generate plausible-looking but incorrect code
- AI may not understand project-specific constraints
- AI might suggest outdated or insecure practices

### Use AI as a Tool, Not a Replacement

- AI is best for boilerplate code, repetitive tasks, or getting started
- Complex logic, security-critical code, and architecture decisions should be human-reviewed

### Appropriate Use Cases

- Generating test cases
- Boilerplate code
- Documentation
- Refactoring suggestions
- Learning about unfamiliar APIs

## For AI Assistants

If you are an AI assistant helping with PitchConnect projects, please follow these additional guidelines:

### First Steps for AI Assistants

- **Read project documentation first**: Always review CONTRIBUTING.md and README.md before starting work
- **Understand the codebase**: Use tools like `codebase-retrieval` to understand the project structure
- **Follow project conventions**: Observe existing patterns in the codebase
- **Plan before coding**: Create a detailed plan before making changes
- **Verify your understanding**: Confirm your understanding of requirements with the user

### Working on Issues

- **Acknowledge the issue**: When asked to work on an issue, acknowledge it and confirm your understanding
- **Follow the GitFlow workflow**: Use the correct branch naming convention and base branches
- **Document your process**: Explain your thought process and decisions as you work
- **Provide progress updates**: Keep the user informed about your progress and any challenges
- **Ask for clarification**: Don't hesitate to ask questions if requirements are unclear

### Issue and Branch Management

- **Always reference issues**: When creating PRs, always reference the relevant issue number using GitHub syntax (e.g., "Fixes #123")
- **Branch naming**: Use the conventional branch naming format:
  - `feature/descriptive-name` for new features
  - `fix/descriptive-name` for bug fixes
  - `docs/descriptive-name` for documentation changes
  - `refactor/descriptive-name` for code refactoring
- **Clean up branches**: Delete feature branches after merging PRs
- **Link related PRs**: If replacing one PR with another, reference the original PR and explain why

### Code Quality and Testing

- **Run pre-commit hooks**: Ensure all pre-commit hooks pass before submitting code
- **Write tests**: Add tests for all new functionality and bug fixes
- **Document your code**: Add docstrings and comments to explain complex logic
- **Follow type hints**: Use proper type annotations for all functions and methods
- **Handle errors gracefully**: Implement proper error handling and logging

### Communication

- **Be explicit**: Clearly state what changes you're making and why
- **Document decisions**: Explain your reasoning, especially for non-obvious choices
- **Provide context**: Reference relevant documentation or discussions
- **Ask questions**: When uncertain, ask for clarification rather than making assumptions
- **Explain limitations**: Be transparent about any limitations in your approach

### GitHub CLI Usage

When using the GitHub CLI with Markdown content, prefer passing content as files rather than streams:

#### Creating Markdown Files for GitHub Content

For complex GitHub content (PR descriptions, issue templates, comments, etc.), create temporary markdown files and use them as input:

**For PR descriptions:**
```bash
# Create a markdown file with your PR description
cat > pr_description.md << 'EOL'
# PR Title

## Description
This PR adds feature X which does Y.

## Changes
- Added new class for X
- Updated tests
- Documentation updates

## Related Issue
Fixes #123

## Type of Change
- [x] New feature
- [ ] Bug fix
EOL

# Create the PR using the file
gh pr create --base develop --head your-branch --title "Add feature X" --body-file pr_description.md

# Clean up
rm pr_description.md
```

**For issue descriptions:**
```bash
# Create a markdown file with your issue description
cat > issue_description.md << 'EOL'
## Description
Detailed description of the issue...

## Steps to Reproduce
1. Step one
2. Step two
3. Step three

## Expected Behavior
What should happen...

## Actual Behavior
What actually happens...
EOL

# Create the issue using the file
gh issue create --title "Bug: Something is broken" --body-file issue_description.md

# Clean up
rm issue_description.md
```

**For comments:**
```bash
# Create a markdown file with your comment
cat > comment.md << 'EOL'
I've reviewed this PR and have the following feedback:

## Code Quality
- The function on line 42 could be simplified
- Good test coverage overall

## Suggestions
```python
# Instead of this:
def complex_function(x, y):
    return x * 2 + y * 3

# Consider this:
def complex_function(x, y):
    return 2*x + 3*y
```
EOL

# Add a comment to a PR
gh pr comment 123 --body-file comment.md

# Clean up
rm comment.md

### PR Descriptions

- **Be comprehensive**: Include all relevant details
- **Use structured format**: Follow the PR template
- **Include testing instructions**: Explain how to test the changes
- **List dependencies**: Mention any new dependencies or requirements
- **Reference issues**: Always link to related issues
- **Describe security implications**: Note any security considerations

### Security Considerations

- **Validate inputs**: Always validate user inputs and file paths
- **Use secure coding practices**: Follow security best practices
- **Consider edge cases**: Think about potential security implications
- **Report security concerns**: Highlight any security issues you identify

### Continuous Improvement

- **Learn from feedback**: Incorporate feedback into future contributions
- **Adapt to project conventions**: Follow established patterns in the codebase
- **Suggest improvements**: Identify opportunities to improve the contribution process
- **Document your learnings**: Share insights that might help future contributors

By following these guidelines, both human and AI contributors can work together effectively to improve PitchConnect projects.
