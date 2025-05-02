# AI Assistant Memories

This document contains important information for AI assistants working with this repository. When starting a new session, AI assistants should review this document to recall important lessons and best practices.

## Command Line Best Practices

### File Editing

1. **For large text replacements, use `awk` instead of `str-replace-editor`**:
   ```bash
   # Replace lines START-END with content from FILE
   awk 'NR<START{print} NR==START{system("cat FILE")} NR>END{print}' original.md > new.md && mv new.md original.md
   ```

2. **Break down complex text manipulations into steps with temporary files**:
   ```bash
   # Extract part before the section
   sed -n '1,START-1p' original.md > temp.md
   
   # Add new content
   cat new_content.md >> temp.md
   
   # Add part after the section
   sed -n 'END+1,$p' original.md >> temp.md
   
   # Replace original
   mv temp.md original.md
   ```

3. **Always use quotes around variables in shell scripts**:
   ```bash
   # Good
   echo "$variable"
   
   # Bad
   echo $variable
   ```

### GitHub Operations

1. **Create labels one by one with error handling**:
   ```bash
   gh api repos/Owner/Repo/labels -X POST -f name="label-name" -f color="color-code" -f description="Label description" || true
   ```

2. **Check if labels exist before creating them**:
   ```bash
   gh label list | grep "label-name" || gh api repos/Owner/Repo/labels -X POST -f name="label-name" -f color="color-code" -f description="Label description"
   ```

3. **Use direct API calls for immediate actions, workflows for future automation**:
   ```bash
   # Immediate action
   gh api repos/Owner/Repo/issues/123/labels -X POST -d '{"labels":["label-name"]}'
   
   # Future automation (workflow)
   gh workflow run workflow-name.yml
   ```

### Repository Navigation

1. **Use absolute paths when working with multiple repositories**:
   ```bash
   cat /tmp/repo1/file.md > /tmp/repo2/file.md
   ```

2. **Be explicit about which repository you're working with**:
   ```bash
   cd /tmp/repo1 && gh issue list
   cd /tmp/repo2 && gh issue list
   ```

3. **Clone repositories to specific directories**:
   ```bash
   gh repo clone Owner/Repo1 /tmp/repo1
   gh repo clone Owner/Repo2 /tmp/repo2
   ```

## Common Pitfalls to Avoid

1. **Don't use complex chains of `sed` commands** - they're hard to debug
2. **Don't assume newly merged workflow files are immediately available** - there's a delay
3. **Don't try to create all labels at once** - do them one by one with error handling
4. **Don't edit files in-place for complex changes** - use temporary files
5. **Don't forget to check which repository you're working in** - especially when switching between multiple repositories

## Repository-Specific Information

### Label System

This repository uses a standardized label system:

1. **Status Labels**:
   - `triage` - Needs initial review by maintainers (removed after triage)
   - `ready-for-development` - Triaged and ready for someone to work on
   - `in-progress` - Being worked on in a draft PR
   - `review-ready` - Work complete and ready for review
   - `merged-to-develop` - Merged to develop branch
   - `released` - Released to production

2. **Type Labels**:
   - `bug`, `enhancement`, `documentation`, `refactor`, `test`

3. **Priority Labels**:
   - `priority:high`, `priority:medium`, `priority:low`

4. **Complexity Labels**:
   - `complexity:easy`, `complexity:medium`, `complexity:hard`

5. **Additional Labels**:
   - `good-first-issue`, `help-wanted`, `blocked`, `discussion`, `wontfix`

### Issue Lifecycle

1. New issue → `triage`
2. After maintainer review → `ready-for-development` (remove `triage`)
3. When work begins → `in-progress` (remove `ready-for-development`)
4. When PR is ready → `review-ready` (remove `in-progress`)
5. When merged to develop → `merged-to-develop` (remove `review-ready`)
6. When released → `released` (remove `merged-to-develop`)
