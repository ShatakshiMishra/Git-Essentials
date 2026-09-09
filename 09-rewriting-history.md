# 09 · Rewriting History

Powerful, tidy, and a little dangerous. These commands **change existing
commits**. The golden rule:

> 🚨 **Only rewrite history that you haven't shared.** Rewriting pushed commits
> forces everyone else to untangle their copies.

## `git commit --amend` — fix the last commit

```bash
# Change the last commit's message
git commit --amend -m "Better message"

# Add a forgotten file to the last commit
git add forgotten.txt
git commit --amend --no-edit    # keep the same message
```

`--amend` replaces the previous commit with a new one. If you already pushed,
you'll need `git push --force-with-lease`.

## `git rebase` — replay commits onto a new base

Rebasing moves your branch's commits so they start from a different point —
giving a clean, linear history instead of merge commits.

```bash
git switch feature
git rebase main         # replay feature's commits on top of latest main
```

Compared to merge:
- **Merge** preserves the true history (with a merge commit).
- **Rebase** rewrites it to look like you started from the latest `main`.

If conflicts appear during a rebase:

```bash
# fix the conflicted files, then:
git add <file>
git rebase --continue
# or bail out entirely:
git rebase --abort
```

## Interactive rebase — clean up a messy branch

The Swiss-army knife. Squash, reorder, edit, or drop commits before sharing.

```bash
git rebase -i HEAD~4     # edit the last 4 commits
```

You'll get an editor listing them:

```
pick a1b2c3d Add feature
squash b4d5e6f Fix typo          # fold into previous commit
reword c7d8e9f Update tests      # change this message
drop  d0e1f2a Debug print        # remove this commit entirely
```

Change `pick` to:
- `reword` — keep the commit, change its message
- `squash` (`s`) — merge into the commit above, combine messages
- `fixup` (`f`) — like squash but discard this message
- `edit` (`e`) — pause to amend the commit's content
- `drop` — delete the commit
- reorder lines to reorder commits

Save and close — Git replays them your way.

## `git cherry-pick` — copy a single commit

Grab one commit from another branch without merging the whole thing.

```bash
git cherry-pick a1b2c3d              # apply that commit here
git cherry-pick a1b2c3d b4d5e6f      # several commits
git cherry-pick main~4..main         # a range
git cherry-pick --no-commit a1b2c3d  # apply changes but don't commit yet
```

Great for backporting a bugfix to a release branch.

---
Next → [10 · Tags & Releases](10-tags-and-releases.md)
