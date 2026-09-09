# 06 · Remotes

A **remote** is a copy of your repo hosted elsewhere (GitHub, GitLab, a
server). It's how you collaborate. The default remote is usually named
`origin`.

## `git remote` — manage connections

```bash
git remote -v                    # list remotes + their URLs
git remote add origin <url>      # connect a new repo to a remote
git remote remove origin         # disconnect
git remote rename origin upstream
git remote set-url origin <url>  # change the URL (e.g. https → ssh)
git remote show origin           # detailed info
```

## `git fetch` — download, don't merge

Grabs new commits from the remote but **doesn't touch your working files**.
Safe to run anytime. Updates the `origin/*` pointers.

```bash
git fetch                # from the default remote
git fetch origin
git fetch --all          # from every remote
git fetch -p             # also prune deleted remote branches
```

After fetching, compare before merging:

```bash
git log HEAD..origin/main --oneline   # what's new on the remote?
```

## `git pull` — fetch + integrate

`pull` = `fetch` + `merge` (or `rebase`). It downloads *and* updates your
current branch.

```bash
git pull                       # fetch + merge into current branch
git pull --rebase              # fetch + rebase (linear history, no merge commit)
git pull origin main           # explicit
```

> **Merge vs rebase pull:** `--rebase` replays your local commits on top of
> the remote's, keeping history straight. Many teams set this as the default:
> `git config --global pull.rebase true`.

## `git push` — upload your commits

Sends your local commits to the remote.

```bash
git push                       # push current branch to its tracked remote
git push origin main           # explicit branch

# First push of a new branch — set the upstream link so future
# 'git push' / 'git pull' work with no arguments:
git push -u origin new-feature

git push --tags                # push your tags too (see Lesson 10)
git push origin --delete old-branch   # delete a branch on the remote
```

### ⚠️ Force pushing
If you rewrote history (rebase, amend — see [Lesson 09](09-rewriting-history.md)),
a normal push is rejected. Force it — carefully:

```bash
git push --force-with-lease    # SAFER: refuses if someone else pushed meanwhile
git push --force               # blunt hammer — can erase others' work ⚠️
```

**Never force-push a shared branch** like `main` unless the whole team agrees.

## Tracking branches

A "tracking" branch is a local branch linked to a remote one, so `push`/`pull`
know where to go.

```bash
git branch -vv                        # see which local tracks which remote
git branch -u origin/main             # set upstream for current branch
git switch -c feat origin/feat        # create local branch tracking a remote one
```

---
Next → [07 · Undoing Things](07-undoing-things.md)
