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
