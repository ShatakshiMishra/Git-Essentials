# 03 · The Basic Cycle

This is the loop you'll run hundreds of times a day:

```
edit files → git add → git commit → (repeat)
```

## `git status` — your compass

Run it constantly. It tells you what's changed, what's staged, and what to do next.

```bash
git status
git status -s        # short format (compact)
```

Files fall into three buckets:
- **Untracked** — Git has never seen this file.
- **Modified** — tracked file changed but not staged.
- **Staged** — marked to go into the next commit.

## `git add` — stage changes

Puts changes into the staging area (the "shopping cart").

```bash
git add file.txt         # one file
git add src/             # a whole folder
git add .                # everything in the current directory
git add -A               # every change in the repo (incl. deletions)
git add -p               # interactively pick chunks — great for tidy commits
```

## `git commit` — save a snapshot

Records everything staged as a permanent point in history.

```bash
git commit -m "Add login form"
```

Other forms:

```bash
# Stage all *tracked* modified files AND commit in one step
# (does NOT add brand-new untracked files)
git commit -am "Fix typo in header"

# Open your editor to write a longer, multi-line message
git commit
```

### Writing good messages
A short summary line (≤ 50 chars), imperative mood ("Add", not "Added"):

```
Add password reset endpoint

Users can now request a reset link by email. Tokens expire
after 1 hour. Closes #42.
```

## `.gitignore` — tell Git what to skip

A file listing patterns Git should never track (build output, secrets, junk).

```bash
# .gitignore
node_modules/
*.log
.env
.DS_Store
dist/
```

- `*.log` — any file ending in `.log`
- `build/` — a whole folder
- `!keep.log` — an exception (do track this one)

> **Already tracked a file by mistake?** `.gitignore` won't help — Git only
> ignores *untracked* files. Stop tracking it with:
> ```bash
> git rm --cached secret.env
> ```

## Removing & moving files

```bash
git rm file.txt          # delete the file AND stage the deletion
git rm --cached file.txt # stop tracking, but keep the file on disk
git mv old.txt new.txt   # rename (= mv + git add, in one step)
```

---
Next → [04 · Inspecting History](04-inspecting-history.md)
