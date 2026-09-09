# 10 · Tags & Releases

A **tag** is a permanent bookmark for a specific commit — usually a release
version like `v1.0.0`. Unlike branches, tags don't move.

## Two kinds of tags

- **Lightweight** — just a name pointing at a commit.
- **Annotated** — a full object with author, date, message (and can be signed).
  **Use annotated for releases.**

```bash
# Annotated (recommended for versions)
git tag -a v1.0.0 -m "First stable release"

# Lightweight (quick private bookmark)
git tag v1.0.0-beta

# Tag an OLD commit, not just the current one
git tag -a v0.9.0 a1b2c3d -m "Retroactive tag"
```

## Listing & inspecting

```bash
git tag                    # list all tags
git tag -l "v1.*"          # filter by pattern
git show v1.0.0            # see what a tag points to + its message
```

## Sharing tags

Tags are **not** pushed by default — you must push them explicitly.

```bash
git push origin v1.0.0     # push one tag
git push origin --tags     # push all tags
git push --follow-tags     # push commits + annotated tags together
```

## Deleting tags

```bash
git tag -d v1.0.0                    # delete locally
git push origin --delete v1.0.0      # delete on the remote
```

## Checking out a tag

```bash
git switch --detach v1.0.0    # look at the code as of that release
# You're now in "detached HEAD" — to work from here, branch off:
git switch -c hotfix-v1.0.1
```

## Semantic versioning (the common convention)

```
v MAJOR . MINOR . PATCH      e.g. v2.4.1
  |       |       └── bug fixes, backward compatible
  |       └────────── new features, backward compatible
  └────────────────── breaking changes
```

---
Next → [11 · Rescue & Debug](11-rescue-and-debug.md)
