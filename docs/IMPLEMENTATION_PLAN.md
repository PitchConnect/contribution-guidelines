# GitHub Actions Implementation Plan for GitFlow Repositories

This document outlines the plan for implementing GitHub Actions workflows across all repositories, with special consideration for repositories using GitFlow.

## Important: GitFlow Considerations

For repositories using GitFlow with both `main` and `develop` as long-living branches:

**⚠️ CRITICAL: Changes must be implemented on BOTH branches ⚠️**

1. **Both Branches Need Automation**: 
   - GitHub Actions workflows must be added to both `main` and `develop` branches
   - CONTRIBUTING.md updates must be applied to both branches
   - Label creation must be run on both branches

2. **Implementation Process for GitFlow Repos**:
   - First implement on `develop` branch
   - Create a separate PR to merge the same changes to `main` branch
   - Do not rely on normal release process to eventually get these changes to `main`

3. **Rationale**:
   - Issues and PRs can target either branch
   - Automation needs to be present on both branches to work correctly
   - Waiting for a release cycle could leave `main` without automation for too long

## Approach

We're taking a two-phase approach:

1. **Phase 1 (Immediate)**: Implement standalone workflows in each repository
2. **Phase 2 (Future)**: Migrate to organization-wide reusable workflows

This approach allows us to get the benefits of automation immediately while setting up for easier maintenance in the future.

## Phase 1: Standalone Workflows

### Workflows to Implement

1. **Issue Labeler**: Automatically adds a "triage" label to new issues
2. **Contributing Guidelines Reminder**: Checks if issues/PRs reference CONTRIBUTING.md
3. **PR Status Tracker**: Updates issue labels based on PR status
4. **Label Creator**: Creates standard labels in repositories
5. **CI Failure Reminder**: Reminds about pre-commit hooks on CI failure
6. **Release PR Generator**: Generates release PRs with all pending issues

### Implementation Steps

1. Use the `add_workflows.sh` script to add these workflows to a repository:
   ```bash
   ./add_workflows.sh <repository-name>
   ```

2. The script will:
   - Clone the repository
   - Add all workflow files
   - Create a feature branch
   - Commit and push the changes
   - Create a PR to the default branch (usually `develop` for GitFlow repos)

3. Review and merge the PR to the default branch

4. **For GitFlow repositories**:
   - Create a second PR to merge the same changes to the `main` branch
   - Review and merge this PR as well
   - Run the Label Creator workflow on both branches

5. Run the Label Creator workflow to create the standard labels

### Priority Repositories

Implement in this order:

1. Active repositories with GitFlow
2. Active repositories without GitFlow
3. Less active repositories

## Phase 2: Organization-Wide Workflows

Once the organization-wide workflows in the `.github` repository are working:

1. Use the `migrate_to_org_workflows.sh` script to migrate a repository:
   ```bash
   ./migrate_to_org_workflows.sh <repository-name>
   ```

2. The script will:
   - Clone the repository
   - Replace standalone workflows with calls to reusable workflows
   - Create a feature branch
   - Commit and push the changes
   - Create a PR to the default branch

3. Review and merge the PR

4. **For GitFlow repositories**:
   - Create a second PR to merge the same changes to the `main` branch
   - Review and merge this PR as well

## Scripts

### add_workflows.sh

Adds standalone workflow files to a repository.

```bash
./add_workflows.sh <repository-name>
```

### migrate_to_org_workflows.sh

Migrates from standalone workflows to organization-wide reusable workflows.

```bash
./migrate_to_org_workflows.sh <repository-name>
```

## Benefits

### Immediate Benefits (Phase 1)

- Automated issue labeling
- Consistent PR status tracking
- Reminders about contribution guidelines
- CI/CD failure reminders
- Automated release PR generation

### Long-term Benefits (Phase 2)

- Reduced duplication across repositories
- Easier maintenance
- Consistent behavior across all repositories
- Future improvements can be made in one place

## Testing

All workflows have been tested in the `workflow-test` repository and are working as expected.

## Migration Path

The migration from Phase 1 to Phase 2 is straightforward:
- The standalone workflows have the same names as the reusable workflows
- The `migrate_to_org_workflows.sh` script handles the migration
- No functionality changes, just using centralized workflows

## Lessons Learned

During implementation, we encountered and resolved several issues:

### 1. Shell Script Variable Handling

- **Issue**: Label names being interpreted as commands in shell scripts
- **Solution**: 
  - Add proper quoting around variables: `echo "$variable"` instead of `echo $variable`
  - Use `-r` flag with `read` to prevent backslash interpretation: `read -r variable`
  - Add debug output to show what's happening during execution

### 2. URL Formatting in curl Commands

- **Issue**: URLs with special characters causing issues in curl commands
- **Solution**: Add quotes around URLs in curl commands
  ```bash
  curl -X POST "https://api.github.com/repos/${{ github.repository }}/issues"
  ```

### 3. Multiline String Handling

- **Issue**: Multiline strings not being properly captured in environment variables
- **Solution**: Use heredoc syntax for multiline strings
  ```bash
  cat << EOF >> $GITHUB_ENV
  VARIABLE_NAME<<EOFMARKER
  multiline
  content
  here
  EOFMARKER
  EOF
  ```

### 4. GitFlow Branch Synchronization

- **Issue**: Automation only working on one branch in GitFlow repositories
- **Solution**: 
  - Implement changes on both `main` and `develop` branches
  - Create separate PRs for each branch
  - Document this requirement clearly

These lessons have been incorporated into the updated workflow templates and scripts to ensure reliable operation across all repositories.
