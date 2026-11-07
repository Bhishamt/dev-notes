# Git

## Undo

```bash
git restore <file>            # discard working-tree changes to a file
git restore --staged <file>   # unstage, keep the edit
git commit --amend --no-edit  # fold staged changes into the last commit
```

## Inspect

```bash
git log --oneline --graph --decorate -20
git diff --stat main...HEAD   # what this branch adds
git blame -w -C -L 40,80 path/to/file
```

## Recover

```bash
git reflog                    # every HEAD move, even after a bad reset
git switch -c rescue <sha>    # branch off a dangling commit
```
