# 05 · Branching & Merging

A **branch** is a movable pointer to a commit — a parallel line of work.
Branches are cheap and fast; use them freely.

## `git branch` — manage branches

```bash
git branch                 # list local branches (* = current)
git branch -a              # include remote branches
git branch -v              # show last commit on each
git branch new-feature     # create a branch (but stay put)
git branch -d old-feature  # delete a merged branch (safe)
git branch -D old-feature  # force-delete (even if unmerged) ⚠️
git branch -m old new      # rename a branch
```

## `git switch` / `git checkout` — move between branches

`switch` is the modern, clearer command. `checkout` is the classic one that
does the same thing (and much more).

```bash
# Switch to an existing branch
git switch main
git checkout main          # equivalent

# Create AND switch in one step
git switch -c new-feature
git checkout -b new-feature   # equivalent

# Jump back to the branch you were just on
git switch -
```

> **Rule of thumb:** use `switch` for branches, `restore` for files (see
> [Lesson 07](07-undoing-things.md)). `checkout` does both jobs, which is why
> it's confusing — the newer commands split it in two.

## `git merge` — combine branches

Bring another branch's work into your current one.

```bash
git switch main            # go to the branch that should RECEIVE the changes
git merge new-feature      # pull new-feature's commits into main
```

Two possible outcomes:

- **Fast-forward** — if `main` hasn't moved, Git just slides the pointer
  forward. No merge commit.
- **Merge commit** — if both branches advanced, Git creates a new commit
  tying them together.

```bash
git merge --no-ff feature  # always make a merge commit (keeps branch visible)
git merge --squash feature # combine all of feature into one staged change
```

## Handling merge conflicts

A conflict happens when both branches changed the **same lines**. Git pauses
and marks the file:

```
<<<<<<< HEAD
your version
=======
their version
>>>>>>> feature
```

To resolve:
1. Open the file, edit it to the version you want, delete the `<<<`/`===`/`>>>` markers.
2. Stage the resolved file: `git add file.txt`
3. Finish the merge: `git commit` (or `git merge --continue`).

Bail out and undo the whole merge:

```bash
git merge --abort
```

## A typical feature-branch workflow

```bash
git switch -c add-search       # 1. branch off
# ...edit, add, commit...
git switch main                # 2. back to main
git pull                       # 3. get latest
git merge add-search           # 4. merge your work in
git branch -d add-search       # 5. clean up
```

---
Next → [06 · Remotes](06-remotes.md)
