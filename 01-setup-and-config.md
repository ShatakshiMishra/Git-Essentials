# 01 · Setup & Config

Before Git can attach your name to commits, you configure it **once** per
machine. Config lives in plain text at `~/.gitconfig`.

## Tell Git who you are (required)

```bash
git config --global user.name "Ada Lovelace"
git config --global user.email "ada@example.com"
```

`--global` = applies to every repo for your user.
Drop `--global` inside a repo to set it for **just that repo** (handy for
work vs. personal email).

## See your settings

```bash
git config --list                 # everything
git config --list --show-origin   # ...and which file each value came from
git config user.name              # one value
```

## Useful one-time settings

```bash
# Default branch name for new repos
git config --global init.defaultBranch main

# Your preferred editor for commit messages
git config --global core.editor "code --wait"   # VS Code
# git config --global core.editor "vim"

# Make 'git pull' rebase instead of merge (cleaner history)
git config --global pull.rebase true

# Colorful output
git config --global color.ui auto
```

## Aliases — make shortcuts

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm "commit -m"
git config --global alias.last "log -1 HEAD"
git config --global alias.lg "log --oneline --graph --all --decorate"
```

Now `git st` runs `git status`, and `git lg` gives you a pretty history graph.

## The three config levels

| Level | Flag | File | Wins over |
|-------|------|------|-----------|
| System | `--system` | `/etc/gitconfig` | (lowest) |
| Global | `--global` | `~/.gitconfig` | system |
| Local | `--local` (default) | `.git/config` | global |

More specific wins. A repo's local setting beats your global one.

---
Next → [02 · Starting a Repo](02-starting-a-repo.md)
