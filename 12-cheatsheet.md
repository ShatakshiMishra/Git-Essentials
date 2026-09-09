# 12 · Cheat Sheet

Everything on one page. `⚠️` = can lose work.

## Setup
```bash
git config --global user.name "Name"
git config --global user.email "you@example.com"
git config --list
git config --global alias.lg "log --oneline --graph --all --decorate"
```

## Start a repo
```bash
git init -b main                 # new repo
git clone <url>                  # copy existing
git clone --depth 1 <url>        # shallow (fast)
```

## Daily cycle
```bash
git status                       # what changed?
git add <file> | . | -A          # stage
git add -p                       # stage interactively
git commit -m "msg"              # save snapshot
git commit -am "msg"             # stage tracked + commit
git rm <file>                    # delete + stage
git mv old new                   # rename
```

## Inspect
```bash
git log --oneline --graph --all  # history graph
git show <commit>                # one commit
git diff                         # unstaged changes
git diff --staged                # staged changes
git blame <file>                 # who wrote each line
```

## Branch & merge
```bash
git branch                       # list
git switch -c <branch>           # create + switch
git switch <branch>              # switch
git switch -                     # previous branch
git merge <branch>               # merge into current
git merge --abort                # cancel a conflicted merge
git branch -d <branch>           # delete (safe)
```

## Remotes
```bash
git remote -v                    # list
git remote add origin <url>      # connect
git fetch                        # download only
git pull                         # fetch + integrate
git pull --rebase                # fetch + rebase
git push                         # upload
git push -u origin <branch>      # first push (set upstream)
git push origin --delete <br>    # delete remote branch
```

## Undo
```bash
git restore <file>               # ⚠️ discard unstaged edits
git restore --staged <file>      # unstage (keep edits)
git commit --amend               # fix last commit
git reset --soft HEAD~1          # uncommit, keep staged
git reset HEAD~1                 # uncommit, keep unstaged
git reset --hard HEAD~1          # ⚠️ uncommit + delete changes
git revert <commit>              # safe undo (new commit)
git clean -fd                    # ⚠️ delete untracked files
```

## Stash
```bash
git stash                        # park changes
git stash -u                     # include untracked
git stash list                   # show stashes
git stash pop                    # re-apply + remove
git stash apply                  # re-apply + keep
git stash drop                   # delete one
```

## Rewrite history (unshared only!)
```bash
git commit --amend --no-edit     # add to last commit
git rebase main                  # replay onto main
git rebase -i HEAD~4             # squash/reorder/edit
git cherry-pick <commit>         # copy one commit
git push --force-with-lease      # ⚠️ push rewritten history safely
```

## Tags
```bash
git tag -a v1.0.0 -m "msg"       # annotated tag
git tag                          # list
git push origin --tags           # share tags
git tag -d v1.0.0                # delete local
```

## Rescue
```bash
git reflog                       # every HEAD move (recover lost work!)
git reset --hard HEAD@{1}        # jump back to a reflog point
git bisect start / good / bad    # find the breaking commit
git log -S "text"                # find commit that changed a string
git fsck --lost-found            # find orphaned commits
```

## The four places
```
Working Dir  --add-->  Staging  --commit-->  Local Repo  --push-->  Remote
     ^                                                                 |
     |______________________ pull / fetch ____________________________|
```

---
← Back to [README](../README.md)
