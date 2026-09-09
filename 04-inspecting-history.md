# 04 · Inspecting History

Git remembers everything. These commands let you look.

## `git log` — the commit history

```bash
git log                        # full history, newest first
git log --oneline              # one line per commit (most useful daily)
git log --oneline --graph --all --decorate   # visual branch graph
git log -5                     # last 5 commits
git log --stat                 # show which files changed + counts
git log -p                     # show the full diff of each commit
```

Filtering:

```bash
git log --author="Ada"         # by author
git log --since="2 weeks ago"  # by date
git log --grep="bugfix"        # search commit messages
git log -- path/to/file.txt    # history of one file
git log main..feature          # commits on feature not yet on main
```

Press `q` to quit the pager.

## `git show` — zoom into one commit

```bash
git show                 # the most recent commit (HEAD)
git show a1b2c3d         # a specific commit by hash
git show HEAD~2          # the commit 2 before HEAD
git show HEAD:file.txt   # a file's contents as of that commit
```

## `git diff` — what exactly changed?

```bash
git diff                 # working dir vs staged (unstaged changes)
git diff --staged        # staged vs last commit (what you're about to commit)
git diff HEAD            # working dir + staged vs last commit
git diff main feature    # difference between two branches
git diff a1b2c3d b4d5e6f # between two commits
git diff --stat          # just a summary of files + line counts
```

## `git blame` — who wrote this line, and when?

```bash
git blame file.txt
git blame -L 10,20 file.txt   # only lines 10–20
```

Great for "why is this here?" — find the commit, then `git show <hash>` to read
the reasoning.

## Referring to commits (revisions)

You'll see these everywhere:

| Reference | Means |
|-----------|-------|
| `HEAD` | The commit you're currently on |
| `HEAD~1` | One commit before HEAD (parent) |
| `HEAD~3` | Three commits back |
| `a1b2c3d` | A commit by its (short) hash |
| `main` | The tip of the `main` branch |
| `origin/main` | The tip of `main` on the remote |

---
Next → [05 · Branching & Merging](05-branching-and-merging.md)
