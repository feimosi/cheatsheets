# Git

## Show the history of the local branch
```git
git reflog --date=local <branch>
```

## Log all commits not reachable from master
```git
git log <branch> --not master
```

## Log commits with file changes stats
```git
git log --stat
```

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

## Succint log
```git
git log --graph --oneline --decorate
```

## Get specific files from another branch
```git
git checkout <branch> -- <paths>
```

## Undo a merge inside a dirty working tree
```git
git reset --merge
```

## Force pull a rebased branch ignoring the local state
```git
git fetch
git reset --hard origin/<branch>
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
git push origin :<branch>
```

## Get the history of specific lines from a file
```git
git blame -L <lines_range> <commit> -- <path>
```

## Edit the previous commit message
```git
git commit --amend -m "New message"
```

## Update the remote branches list
```git
git remote prune origin
```

## Push a new local branch to a remote
```git
git push -u origin <branch>
```

## Unstage a file
```git
git reset <file>
```
___
# Links
* [http://ndpsoftware.com/git-cheatsheet.html](http://ndpsoftware.com/git-cheatsheet.html#loc=workspace;)
