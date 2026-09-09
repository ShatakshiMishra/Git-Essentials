# 08 · Stashing

**Stash** = a clipboard for unfinished work. You're mid-change, but need a
clean working directory *right now* (to switch branches, pull, etc.). Stash
tucks your changes away and gives you back a clean slate.

## The basics

```bash
git stash               # park all tracked changes, revert working dir to clean
git stash list          # see everything you've stashed
git stash pop           # re-apply the most recent stash AND remove it from the list
git stash apply         # re-apply but KEEP it in the list (useful for reuse)
git stash drop          # delete the most recent stash
git stash clear         # delete ALL stashes ⚠️
```

## Useful variants

```bash
git stash -u                        # also stash UNtracked files
git stash -a                        # also stash ignored files too
git stash push -m "half-done navbar"  # give it a descriptive name
git stash push path/to/file.txt     # stash only specific files
```

## Working with multiple stashes

Stashes are a stack: `stash@{0}` is newest.

```bash
git stash list
# stash@{0}: On main: half-done navbar
# stash@{1}: WIP on feature: ...

git stash apply stash@{1}    # apply a specific one
git stash pop stash@{1}      # apply + remove a specific one
git stash show -p stash@{0}  # view the diff of a stash
```

## Turn a stash into a branch

If a stash is getting complex, promote it:

```bash
git stash branch new-feature stash@{0}
```

This creates a branch from where you stashed and applies the stash — no
conflict headaches.

## Typical use

```bash
# You're editing, boss says "hotfix main NOW"
git stash                 # clean slate
git switch main
# ...fix, commit, push the hotfix...
git switch my-work
git stash pop             # back to exactly where you were
```

---
Next → [09 · Rewriting History](09-rewriting-history.md)
