# 02 · Starting a Repo

There are two ways to get a Git repo: **create** a new one, or **copy** an
existing one.

## `git init` — start fresh

Turns the current folder into a Git repo by creating a hidden `.git/` directory.

```bash
mkdir my-project
cd my-project
git init
```

Modern Git prints the default branch name. To start on `main`:

```bash
git init -b main          # newer Git
# or, if that flag isn't supported:
git init && git branch -m main
```

Nothing is tracked yet — `.git/` is just an empty vault. See [Lesson 03](03-the-basic-cycle.md)
to put files into it.

## `git clone` — copy an existing repo

Downloads a full repo (all history) and sets up the remote automatically.

```bash
git clone https://github.com/user/repo.git
```

Handy variations:

```bash
# Clone into a folder named "myapp" instead of "repo"
git clone https://github.com/user/repo.git myapp

# Clone only the latest commit (fast, less history) — a "shallow" clone
git clone --depth 1 https://github.com/user/repo.git

# Clone a specific branch
git clone --branch develop https://github.com/user/repo.git
```

After cloning, the source is saved as a remote called `origin` — see
[Lesson 06](06-remotes.md).

## What's inside `.git/`?

You rarely touch it, but it's good to know it exists:

```bash
ls -a          # you'll see a .git folder
```

It holds every commit, branch, and config for the repo. **Delete `.git/` and
you delete the entire history** (the files themselves stay). To "un-git" a
folder: `rm -rf .git`.

---
Next → [03 · The Basic Cycle](03-the-basic-cycle.md)
