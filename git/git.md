# Git Commands Cheat Sheet

A quick-reference guide for the most commonly used Git commands. Perfect for interviews, daily development, and quick revision.

---

# Search for Text in the Repository

Search for a specific word, function, class, or variable across the repository.

## Syntax

```bash
git grep "keyword"
```

## Example

```bash
git grep "test_update_with_exogenous_variables"
```

**Use Cases**

- Find where a function is defined.
- Locate a variable or class.
- Search through a large codebase quickly.

---

# Branch Management

## List All Local Branches

```bash
git branch
```

---

## List All Branches (Local + Remote)

```bash
git branch -a
```

---

## Create a New Branch

```bash
git branch feature/login
```

---

## Create and Switch to a Branch

```bash
git checkout -b feature/login
```

Or (recommended):

```bash
git switch -c feature/login
```

---

## Switch Branches

```bash
git checkout main
```

Or

```bash
git switch main
```

---

## Rename Current Branch

```bash
git branch -m new_branch_name
```

---

# Delete Branches

## Delete a Merged Branch (Safe)

Git only deletes the branch if it has already been merged.

```bash
git branch -d branch_name
```

Example

```bash
git branch -d feature/login
```

---

## Force Delete a Branch

Deletes the branch even if it hasn't been merged.

```bash
git branch -D branch_name
```

Example

```bash
git branch -D feature/login
```

> ⚠️ Use `-D` carefully because unmerged work may be lost.

---

# Git Stash

Temporarily save your uncommitted work without committing it.

## Save Current Changes

```bash
git stash
```

---

## Save with a Description

```bash
git stash push -m "Fix login bug"
```

---

## List All Stashes

```bash
git stash list
```

---

## Apply Latest Stash

```bash
git stash apply
```

---

## Apply and Remove Latest Stash

```bash
git stash pop
```

---

## Delete a Stash

```bash
git stash drop stash@{0}
```

---

## Clear All Stashes

```bash
git stash clear
```

---

# Inspecting Commits

## Show the Latest Commit

```bash
git show HEAD
```

---

## Show Changed Files Only

Displays which files were modified in the latest commit.

```bash
git show --stat HEAD
```

Example Output

```text
README.md             | 12 +++++++
src/app.py            | 20 +++++++++++++++
tests/test_app.py     | 10 +++++
```

---

## View Commit History

```bash
git log
```

Compact version

```bash
git log --oneline
```

Graph view

```bash
git log --oneline --graph --all
```

---

# Restore Files

Restore a specific file from another branch.

## Syntax

```bash
git checkout branch_name -- file_path
```

Example

```bash
git checkout upstream/main -- sktime/transformations/series/boxcox.py
```

This command replaces your local version of the file with the version from `upstream/main`.

---

# Check Repository Status

Shows staged, unstaged, and untracked files.

```bash
git status
```

---

# Stage Files

Stage a single file

```bash
git add README.md
```

Stage everything

```bash
git add .
```

---

# Commit Changes

```bash
git commit -m "Fix login authentication"
```

---

# Push Changes

```bash
git push origin feature/login
```

---

# Pull Latest Changes

```bash
git pull origin main
```

---

# Fetch Without Merging

Downloads changes without modifying your branch.

```bash
git fetch
```

---

# Clone a Repository

```bash
git clone https://github.com/user/repository.git
```

---

# View Remote Repositories

```bash
git remote -v
```

Example

```text
origin      https://github.com/user/repo.git
upstream    https://github.com/original/repo.git
```

---

# Add an Upstream Repository

```bash
git remote add upstream https://github.com/original/repository.git
```

---

# Sync with Upstream

Fetch latest changes

```bash
git fetch upstream
```

Merge upstream changes

```bash
git merge upstream/main
```

Or rebase

```bash
git rebase upstream/main
```

---

# Undo Changes

## Undo Unstaged Changes

```bash
git restore file_name
```

---

## Unstage a File

```bash
git restore --staged file_name
```

---

## Reset Last Commit (Keep Changes)

```bash
git reset --soft HEAD~1
```

---

## Reset Last Commit (Discard Changes)

```bash
git reset --hard HEAD~1
```

> ⚠️ This permanently deletes uncommitted work.

---

# Compare Changes

Compare current changes

```bash
git diff
```

Compare staged changes

```bash
git diff --staged
```

Compare with another branch

```bash
git diff main
```

---

# Tags

Create a tag

```bash
git tag v1.0
```

List tags

```bash
git tag
```

Push tags

```bash
git push --tags
```

---

# Cherry Pick

Apply a commit from another branch.

```bash
git cherry-pick commit_hash
```

Example

```bash
git cherry-pick a1b2c3d
```

---

# Rebase

Replay your commits on top of another branch.

```bash
git rebase main
```

Interactive rebase

```bash
git rebase -i HEAD~3
```

Common interview question:
> Rebase creates a cleaner, linear history compared to merge.

---

# Merge

Merge another branch into the current branch.

```bash
git merge feature/login
```

---

# Remove a Tracked File

Keep the file locally but remove it from Git tracking.

```bash
git rm --cached file_name
```

---

# Useful Interview Commands

Find the author of each line

```bash
git blame file_name
```

Find who introduced a bug

```bash
git bisect
```

View one-line commit history

```bash
git log --oneline
```

See file changes

```bash
git diff
```

View commit details

```bash
git show commit_hash
```

Search commit messages

```bash
git log --grep="bug"
```

Search code

```bash
git grep "keyword"
```

---

# Daily Git Workflow

```text
1. git pull
2. git checkout -b feature/new-feature
3. Make changes
4. git status
5. git add .
6. git commit -m "Implement new feature"
7. git push origin feature/new-feature
8. Create Pull Request
9. Review
10. Merge
11. git checkout main
12. git pull
13. git branch -d feature/new-feature
```

---

# Interview Tips

## Difference Between Merge and Rebase

| Merge | Rebase |
|--------|--------|
| Preserves history | Creates linear history |
| Creates merge commits | No merge commits |
| Easier to understand | Cleaner commit history |

---

## Difference Between Fetch and Pull

| Fetch | Pull |
|--------|------|
| Downloads changes only | Downloads and merges changes |
| Safe | May create merge conflicts |
| Doesn't modify working directory | Updates current branch |

---

## Difference Between Reset and Restore

| Reset | Restore |
|--------|----------|
| Changes commit history | Restores files |
| Can remove commits | Doesn't remove commits |
| More powerful | Safer for beginners |

---

# Quick Revision Table

| Command | Purpose |
|---------|---------|
| `git status` | Check repository status |
| `git add .` | Stage all changes |
| `git commit -m` | Create a commit |
| `git push` | Upload commits |
| `git pull` | Download and merge |
| `git fetch` | Download changes only |
| `git branch` | List branches |
| `git switch` | Switch branches |
| `git checkout` | Switch branch or restore files |
| `git merge` | Merge branches |
| `git rebase` | Reapply commits on another branch |
| `git stash` | Temporarily save changes |
| `git stash pop` | Restore stashed changes |
| `git diff` | Compare changes |
| `git log` | View commit history |
| `git show` | View commit details |
| `git grep` | Search inside repository |
| `git blame` | See who changed each line |
| `git cherry-pick` | Copy a commit from another branch |
| `git rm --cached` | Stop tracking a file |
| `git tag` | Create release tags |

---

# Pro Tip

For interview preparation, remember these **15 commands** first:

```text
git clone
git status
git add
git commit
git push
git pull
git fetch
git branch
git switch
git checkout
git merge
git rebase
git stash
git diff
git log
```

Mastering these commands covers **around 90% of everyday Git usage** in software engineering jobs and technical interviews.
