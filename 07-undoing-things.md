# 07 · Undoing Things

The scariest part of Git — made simple. The key question is always:
**how far along was the change?**

| Situation | Command |
|-----------|---------|
| Discard edits in a file (not staged) | `git restore <file>` |
| Unstage a file (keep the edits) | `git restore --staged <file>` |
| Fix the last commit's message/content | `git commit --amend` |
| Undo commits but keep the changes | `git reset --soft/--mixed` |
| Throw commits away entirely | `git reset --hard` ⚠️ |
| Undo a commit *safely* (new commit) | `git revert` |
| Delete untracked files/folders | `git clean` |

## `git restore` — fix working files

```bash
git restore file.txt           # discard unstaged changes to file.txt ⚠️
git restore .                  # discard ALL unstaged changes ⚠️
git restore --staged file.txt  # unstage (undo a 'git add'), keep edits
git restore --source=HEAD~2 file.txt   # bring back an old version of a file
```

## `git reset` — move the branch pointer

Resets rewind your branch to an earlier commit. The `--flag` decides what
happens to the changes:

```bash
# Undo the last commit, KEEP changes staged
git reset --soft HEAD~1

# Undo the last commit, keep changes but UNstaged (the default)
git reset --mixed HEAD~1
git reset HEAD~1               # same thing

# Undo the last commit AND discard the changes entirely ⚠️ DESTRUCTIVE
git reset --hard HEAD~1
```

Think of it as three levels of "undo":
- `--soft` → uncommit (changes stay staged)
- `--mixed` → uncommit + unstage (changes stay in files)
- `--hard` → uncommit + unstage + delete changes

## `git revert` — the safe undo

Instead of erasing a commit, `revert` creates a **new** commit that undoes it.
Safe for shared/pushed history because it doesn't rewrite anything.

```bash
git revert HEAD                # undo the last commit with a new commit
git revert a1b2c3d             # undo a specific commit
git revert --no-commit HEAD~3..HEAD   # revert a range, review before committing
```

> **Rule:** `reset` for local, un-pushed work. `revert` for anything you've
> already shared.

## `git clean` — remove untracked files

`reset --hard` doesn't touch untracked files. `clean` does.

```bash
git clean -n     # DRY RUN — show what would be deleted (always do this first)
git clean -f     # delete untracked files
git clean -fd    # delete untracked files AND directories
git clean -fdx   # ...including ignored files (node_modules, etc.) ⚠️
```

## Quick recipes

```bash
# "I committed to main but meant to be on a branch"
git branch my-feature       # bookmark current spot on a new branch
git reset --hard origin/main   # rewind main; work is safe on my-feature
git switch my-feature

# "I want to throw away ALL local changes and match the remote"
git fetch origin
git reset --hard origin/main
git clean -fd
```

Made a mistake with reset? See [Lesson 11 · reflog](11-rescue-and-debug.md) —
almost nothing is truly lost for ~30 days.

---
Next → [08 · Stashing](08-stashing.md)
