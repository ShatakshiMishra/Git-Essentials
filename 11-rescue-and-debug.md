# 11 · Rescue & Debug

When things go wrong, these are your lifelines.

## `git reflog` — the undo history of undos

Git records **every** place `HEAD` has been — even commits you "deleted" with a
bad reset or rebase. This is your safety net.

```bash
git reflog
# a1b2c3d HEAD@{0}: reset: moving to HEAD~3
# e4f5g6h HEAD@{1}: commit: The work I thought I lost
# ...
```

Recover lost work by pointing back to it:

```bash
git reset --hard HEAD@{1}      # go back to where you were before the mistake
# or save it on a new branch:
git branch recovered e4f5g6h
```

> Reflog entries stick around ~90 days for reachable and ~30 for unreachable
> commits. **You can almost always get your work back** — check reflog before
> panicking.

## `git bisect` — find the commit that broke it

Binary-search your history to pinpoint which commit introduced a bug.

```bash
git bisect start
git bisect bad                 # current version is broken
git bisect good v1.0.0         # this old version worked

# Git checks out a commit halfway between. Test it, then tell Git:
git bisect good     # ...if this commit works
git bisect bad      # ...if it's broken

# Repeat. Git narrows it down and names the guilty commit.
git bisect reset               # when done, return to where you started
```

Automate it if you have a test script (0 = good, non-zero = bad):

```bash
git bisect start HEAD v1.0.0
git bisect run ./test.sh
```

## Recovering specific things

```bash
# Restore a file you deleted and committed
git restore --source=HEAD~1 deleted-file.txt

# Find a lost commit that isn't in any branch
git fsck --lost-found

# See what a branch looked like yesterday
git show 'main@{yesterday}'
git show 'HEAD@{2 hours ago}'
```

## Searching the codebase & history

```bash
git grep "TODO"                    # search tracked files (like grep, but Git-aware)
git grep -n "functionName"         # with line numbers
git log -S "oldFunctionName"       # find commits that added/removed a string
git log -G "regex"                 # find commits whose diff matches a regex
```

## Diagnosing state

```bash
git status                 # always start here
git log --oneline --graph --all    # visualize where every branch is
git branch -vv             # tracking + ahead/behind counts
git remote show origin     # remote branch relationships
```

---
Next → [12 · Cheat Sheet](12-cheatsheet.md)
