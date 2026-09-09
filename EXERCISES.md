# 🏋️ Hands-On Exercises

The only way to learn Git is to run it. Do these in a throwaway folder —
nothing here can hurt a real project.

```bash
mkdir git-practice && cd git-practice
```

You can always start over: `cd .. && rm -rf git-practice`.

---

## Exercise 1 — Your first commit
1. `git init -b main`
2. Create a file: `echo "hello" > notes.txt`
3. Check `git status` — notice `notes.txt` is *untracked*.
4. `git add notes.txt`, then `git status` again — now it's *staged*.
5. `git commit -m "Add notes"`
6. `git log --oneline` — see your commit.

## Exercise 2 — Staging vs. working directory
1. Edit the file: `echo "world" >> notes.txt`
2. `git diff` — see the unstaged change.
3. `git add notes.txt`, then `git diff` (empty) vs `git diff --staged` (shows it).
4. Undo the staging: `git restore --staged notes.txt`.
5. Discard the edit entirely: `git restore notes.txt`. Confirm it's gone.

## Exercise 3 — Branching
1. `git switch -c feature`
2. Add a file, commit it.
3. `git switch main` — the file disappears (it lives on `feature`).
4. `git merge feature` — it's back.
5. `git log --oneline --graph --all` — see the shape of history.

## Exercise 4 — Merge conflict (on purpose)
1. On `main`: `echo "line from main" > shared.txt`, commit.
2. `git switch -c other`, change the same line: `echo "line from other" > shared.txt`, commit.
3. `git switch main`, change it differently, commit.
4. `git merge other` → **conflict!**
5. Open `shared.txt`, resolve the `<<<<`/`====`/`>>>>` markers, `git add shared.txt`, `git commit`.

## Exercise 5 — Undoing a commit
1. Make a bad commit.
2. `git reset --soft HEAD~1` — commit undone, changes still staged.
3. Re-commit, then try `git revert HEAD` — watch it make a *new* undo commit.
4. Compare the two approaches in `git log`.

## Exercise 6 — Stashing
1. Start editing a file (don't commit).
2. `git stash` — working dir goes clean.
3. `git stash list`, then `git stash pop` — your edits return.

## Exercise 7 — Rescue with reflog
1. Note a commit hash from `git log`.
2. `git reset --hard HEAD~2` — "lose" two commits.
3. `git reflog` — find them still listed.
4. `git reset --hard HEAD@{1}` — bring them back. 🎉

---

**Done?** You now know more Git than most people use daily. Keep the
[cheat sheet](lessons/12-cheatsheet.md) handy.
