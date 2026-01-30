# Git Workflow Guide: WIP Branches and Squash Merges

## Overview

This guide explains how to work with Work-In-Progress (WIP) branches and use squash merges effectively in your development workflow.

## Working with WIP Branches

### What is a WIP Branch?

A WIP (Work In Progress) branch is a feature branch that contains incomplete or experimental work. It's a way to share progress, get early feedback, or collaborate on unfinished features.

### Creating a WIP Branch

```bash
# Create and switch to a new WIP branch
git checkout -b wip/feature-name

# Make your changes
# ...

# Commit your work (can be multiple commits)
git add .
git commit -m "WIP: Initial implementation of feature"

# Push to remote
git push origin wip/feature-name
```

### Best Practices for WIP Branches

1. **Use clear naming**: Prefix branches with `wip/` to indicate work in progress
2. **Commit often**: Make frequent commits to save your work
3. **Push regularly**: Push to remote to backup your work
4. **Use descriptive messages**: Even WIP commits should have meaningful messages
5. **Mark PRs as draft**: Open draft pull requests to get early feedback

## Squash Merging

### What is a Squash Merge?

A squash merge combines all commits from a feature branch into a single commit when merging into the main branch. This keeps the main branch history clean and linear.

### Benefits of Squash Merging

- **Clean history**: One commit per feature instead of many small commits
- **Easy rollback**: Revert an entire feature with one revert
- **Better readability**: Main branch shows high-level changes
- **Removes WIP commits**: All experimental commits are consolidated

### How to Squash Merge

#### Via GitHub Pull Request

1. Open a pull request from your WIP branch to main
2. Get your code reviewed
3. Click "Squash and merge" button
4. Edit the commit message to summarize all changes
5. Confirm the merge

#### Via Command Line

```bash
# Switch to main branch
git checkout main

# Pull latest changes
git pull origin main

# Merge with squash
git merge --squash wip/feature-name

# Commit the squashed changes
git commit -m "Add feature: descriptive message"

# Push to remote
git push origin main
```

## Complete Workflow Example

Here's a complete workflow from creating a WIP branch to squash merging:

```bash
# 1. Create WIP branch
git checkout -b wip/add-data-visualization
git push -u origin wip/add-data-visualization

# 2. Make multiple commits as you work
git add notebook.ipynb
git commit -m "WIP: Add initial chart"

git add notebook.ipynb
git commit -m "WIP: Improve chart styling"

git add notebook.ipynb
git commit -m "WIP: Add second visualization"

git push

# 3. Open draft PR on GitHub for early feedback

# 4. Continue working based on feedback
git add notebook.ipynb
git commit -m "WIP: Address review comments"
git push

# 5. When ready, mark PR as ready for review

# 6. After approval, use "Squash and merge" on GitHub
#    All commits become one clean commit on main

# 7. Clean up local branch
git checkout main
git pull
git branch -d wip/add-data-visualization
```

## Tips for Writing Good Squash Commit Messages

When squashing, write a commit message that:

1. **Summarizes the feature**: "Add interactive data visualizations for population analysis"
2. **Explains the why**: "These visualizations help users understand trends in the data"
3. **Lists key changes** (optional):
   ```
   Add interactive data visualizations for population analysis
   
   - Created bar chart for population by region
   - Added line chart for population trends over time
   - Implemented interactive filters for data exploration
   ```

## Cleaning Up After Merge

```bash
# Delete local branch
git branch -d wip/feature-name

# Delete remote branch (if not auto-deleted by GitHub)
git push origin --delete wip/feature-name
```

## When NOT to Squash Merge

- When you want to preserve detailed commit history
- When working on long-lived feature branches with multiple contributors
- When commits are already well-organized and meaningful

## Summary

- Use WIP branches for experimental or incomplete work
- Commit and push frequently to save progress
- Open draft PRs for early feedback
- Use squash merge to keep main branch history clean
- Write good squash commit messages that summarize the feature
