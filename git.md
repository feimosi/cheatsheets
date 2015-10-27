# Git

## Determine when a branch was created
```git
git reflog --date=local <branch>
```
Show the history of the branch. The last entry in this list is the point at which you created the branch.
```git
git log <branch> --not master
```
A list of commits reachable from <branch> that are not reachable from master.

## List remote branches with last committer sorted by date
```git
git for-each-ref --format='%(committerdate)%09%(authorname)%09%(refname)' | \
sort -k5n -k2M -k3n -k4n | grep remotes | \
awk -F "\t" '{ printf "%-32s %-27s %s\n", $1, $2, $3 }'
```

## Add alias
```git
git config --global alias.<name> <command>
```

## List all aliases
```git
git config --get-regexp alias
```

## See the files affected by a commit
```git
git diff-tree -r --name-only --no-commit-id <commit>
```

## Convenient log
```git
git log --graph --oneline
```

## Get specific files from another branch
```git
git checkout <branch> -- <paths>
```

## Undo a merge
```git
git reset --hard
```

## Undo a merge inside a dirty working tree
```git
git reset --merge
```

## Pull a rebased branch ignoring the local state
```git
git reset --hard origin/<rebased>
```

## Show `remote` information (including URL)
```git
git remote show origin
```

## Show only the staged changes 
```git
git diff --staged
```

## Delete a remote branch
```git
git push origin --delete <branch>
```

## Get the history of specific lines from a file
```git
git blame -L <lines_range> <commit> -- <path>
```
