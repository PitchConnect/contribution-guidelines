# CONTRIBUTING.md Sync Workflow

This document describes how to set up automatic synchronization of the central CONTRIBUTING.md file to individual repositories.

## Overview

To ensure consistency across all repositories, we use a GitHub Actions workflow that automatically syncs the CONTRIBUTING.md file from this central repository to individual repositories while preserving any repository-specific guidelines.

## How It Works

1. The workflow downloads the latest CONTRIBUTING.md from this central repository
2. It preserves the "Repository-Specific Guidelines" section from the local CONTRIBUTING.md
3. It updates the local CONTRIBUTING.md with the latest content from the central repository
4. It commits and pushes the changes if any

## Setup Instructions

To set up the sync workflow in a repository:

1. Create a file at `.github/workflows/contributing-sync.yml` with the following content:

```yaml
name: Sync CONTRIBUTING.md

on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * 0'  # Run every Sunday at midnight

jobs:
  sync-contributing:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
        
      - name: Get source CONTRIBUTING.md
        run: |
          # Download source CONTRIBUTING.md
          curl -s -H "Authorization: token ${{ secrets.GITHUB_TOKEN }}" \
            -H "Accept: application/vnd.github.v3.raw" \
            "https://api.github.com/repos/PitchConnect/contribution-guidelines/contents/CONTRIBUTING.md" > source_contributing.md
          
          # Check if target CONTRIBUTING.md exists
          if [ -f "CONTRIBUTING.md" ]; then
            # Extract repository-specific section
            REPO_SPECIFIC=$(sed -n "/^## Repository-Specific Guidelines/,/<!-- END COMMON SECTION -->/p" "CONTRIBUTING.md" || echo "## Repository-Specific Guidelines\n\n<!-- Add repository-specific guidelines here -->\n\n<!-- END COMMON SECTION -->")
            
            # Replace repository-specific section in source file
            sed -i "/^## Repository-Specific Guidelines/,/<!-- END COMMON SECTION -->/c\\$REPO_SPECIFIC" source_contributing.md
          fi
          
          # Update target CONTRIBUTING.md
          mv source_contributing.md "CONTRIBUTING.md"
          
          # Commit changes if any
          git config user.name "GitHub Actions"
          git config user.email "actions@github.com"
          git add "CONTRIBUTING.md"
          git diff --staged --quiet || git commit -m "Update CONTRIBUTING.md from contribution-guidelines"
          git push
```

2. Commit and push the workflow file to the repository
3. Ensure the repository has a CONTRIBUTING.md file with a "Repository-Specific Guidelines" section

## Repository-Specific Guidelines Section

For the sync to work properly, each repository's CONTRIBUTING.md file should have a section like this:

```markdown
## Repository-Specific Guidelines

<!-- Add repository-specific guidelines here -->

<!-- END COMMON SECTION -->
```

This section will be preserved during the sync process, allowing each repository to maintain its own specific guidelines while keeping the common sections in sync.

## Manual Trigger

To manually trigger the sync workflow:

1. Go to the repository on GitHub
2. Click on the "Actions" tab
3. Select the "Sync CONTRIBUTING.md" workflow
4. Click on "Run workflow"
5. Select the branch (usually "main" or "develop")
6. Click "Run workflow"

## Automatic Schedule

The workflow is configured to run automatically every Sunday at midnight. This schedule can be adjusted by modifying the `cron` expression in the workflow file.

## Troubleshooting

If the sync workflow fails, check the following:

1. Ensure the repository has the necessary permissions for the GitHub token
2. Verify that the CONTRIBUTING.md file has the correct "Repository-Specific Guidelines" section
3. Check the workflow logs for any error messages

## Implementation Status

| Repository | Sync Workflow Implemented | Last Synced |
|------------|---------------------------|------------|
| fogis-api-client-python | Yes (PR #169) | N/A |
| [Add other repositories here] | | |
