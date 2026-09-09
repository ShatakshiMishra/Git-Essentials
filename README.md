# The Git Command Handbook 📚

A teaching repository. Every common Git command, grouped by what you're
actually trying to do, with plain-English explanations and copy-pasteable
examples.

> **How to use this repo**
> Read the lessons in order if you're new, or jump to the one you need.
> Each lesson is a standalone Markdown file. Try the commands in a throwaway
> folder — you can always `rm -rf` and start over.

## The mental model (read this first)

Git moves your work through **four places**:

```
  Working Directory  →  Staging Area  →  Local Repo  →  Remote Repo
   (your files)          (git add)       (git commit)    (git push)
        ↑___________________________________________________|
                          (git pull / fetch)
```

- **Working directory** — the actual files you edit.
- **Staging area (index)** — a "shopping cart" of changes you've marked to save.
- **Local repository** — the committed history on your machine (`.git/`).
- **Remote repository** — the shared copy (e.g. GitHub, GitLab).

Almost every command below just moves changes between these four places.

## Lessons

| # | Lesson | What you'll learn |
|---|--------|-------------------|
| 01 | [Setup & Config](lessons/01-setup-and-config.md) | Identity, editor, aliases, `git config` |
| 02 | [Starting a Repo](lessons/02-starting-a-repo.md) | `init`, `clone` |
| 03 | [The Basic Cycle](lessons/03-the-basic-cycle.md) | `status`, `add`, `commit`, `.gitignore` |
| 04 | [Inspecting History](lessons/04-inspecting-history.md) | `log`, `show`, `diff`, `blame` |
| 05 | [Branching & Merging](lessons/05-branching-and-merging.md) | `branch`, `checkout`, `switch`, `merge` |
| 06 | [Remotes](lessons/06-remotes.md) | `remote`, `fetch`, `pull`, `push` |
| 07 | [Undoing Things](lessons/07-undoing-things.md) | `restore`, `reset`, `revert`, `clean` |
| 08 | [Stashing](lessons/08-stashing.md) | `stash` — parking work in progress |
| 09 | [Rewriting History](lessons/09-rewriting-history.md) | `rebase`, `commit --amend`, `cherry-pick` |
| 10 | [Tags & Releases](lessons/10-tags-and-releases.md) | `tag` — marking versions |
| 11 | [Rescue & Debug](lessons/11-rescue-and-debug.md) | `reflog`, `bisect`, recovering lost work |
| 12 | [Cheat Sheet](lessons/12-cheatsheet.md) | Everything on one page |

## The absolute minimum

If you learn only five commands, learn these:

```bash
git status          # What's going on right now?
git add <file>      # Stage a change to be saved
git commit -m "msg" # Save staged changes to history
git pull            # Get everyone else's changes
git push            # Share your changes
```

---
*This repo is itself a Git repo — poke around with `git log` to see how the
lessons were committed.*
