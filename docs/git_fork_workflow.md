# Git Fork Workflow

Merge upstream changes while preserving your `.devcontainer`.

## 1. Reconnaissance

```bash
git branch -a       # List all branches
git remote -v       # Show remotes
```

## 2. Configure Remotes (one-time setup)

```bash
git remote rename origin upstream                       # Boss's repo becomes 'upstream'
git remote add origin https://github.com/dan-burk/vibe.git   # Your fork becomes 'origin'
```

## 3. Set Branch Tracking (one-time setup)

```bash
git branch --set-upstream-to=origin/main main   # Track your fork, not upstream
git branch -vv                                   # Verify: should show [origin/main]
```

## 4. Sync and Restore .devcontainer

```bash
git fetch origin                           # Download latest
git checkout main                          # Switch to main
git checkout temp -- .devcontainer/        # Copy .devcontainer from temp branch
```

## 5. Commit and Push

```bash
git add .devcontainer/
git commit -m "Restore .devcontainer from temp branch"
git status
git push
```

## Quick Reference

| Command | What it does |
|---------|--------------|
| `git fetch origin` | Downloads updates, doesn't change files |
| `git checkout branch` | Switches to a branch |
| `git checkout branch -- path/` | Copies files from another branch |
| `git branch -vv` | Shows branches and what they track |
| `git remote -v` | Shows remotes and their URLs |
| `git reset HEAD~1` | Undo last commit (keeps files) |
| `git reset --hard HEAD~1` | Undo last commit (discards files) |
