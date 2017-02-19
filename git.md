# Git

## Get the history of specific lines from a file
```git
git blame -L <lines_range> <commit> -- <path>
```

## Change the remote a branch is tracking
```git
git branch <branch> -u <remote>/<branch>
```

## Stop tracking a remote branch
```git
git branch --unset-upstream
```

## Get specific files from another branch
```git
git checkout <branch> -- <paths>
```

## Check out any of the previous branches
```git
git checkout @{-<number>}
```

## Remove local (untracked) files
```git
git clean -f -d
```

## Edit the previous commit message
```git
git commit --amend -m "New message"
```

## Add alias
```git
git config --global alias.<name> <command>
```

## List all aliases
```git
git config --get-regexp alias
```

## Show only the staged changes 
```git
git diff --staged
```

## Compare two branches by their tips
```git
git diff <branch-1>..<branch-2>
```

## See the files affected by a commit
```git
git diff-tree -r --name-only --no-commit-id <commit>
```

## List remote branches with last committer sorted by date
```git
git for-each-ref --format='%(committerdate)%09%(authorname)%09%(refname)' | \
sort -k5n -k2M -k3n -k4n | grep remotes | \
awk -F "\t" '{ printf "%-32s %-27s %s\n", $1, $2, $3 }'
```

## Log all commits not reachable from master
```git
git log <branch> --not master
```

## Log commits with file changes stats
```git
git log --stat
```

## Search for changes containing given string
```git
git log -S '<search string>'
```

## Log only merge commits
```git
git log --merges
```

## Succint log
```git
git log --graph --oneline --decorate
```

## Squash all branch commits into one and merge them into current branch
```git
git merge --squash <branch>
```

## Delete a remote branch
```git
git push origin --delete <branch>
git push origin :<branch>
```

## Push a new local branch to a remote
```git
git push -u origin <branch>
```

## Rebase from the common ancestor
```git
git rebase --onto master <ancestor_branch> <branch>
```

## Show the history of the local branch
```git
git reflog --date=local <branch>
```
## Use new remote repository
```git
git remote add <remote> git://path/to/repo.git
git fetch <remote>
git checkout --track <remote>/<branch>
```

## Show `remote` information (including URL)
```git
git remote show origin
```
## Change the remote's URL
```git
git remote set-url origin git@github.com/USERNAME/OTHERREPOSITORY.git
```

## Update the remote branches list
```git
git remote prune origin
```

## Undo a merge inside a dirty working tree
```git
git reset --merge
```

## Unstage a file
```git
git reset <file>
```

## Force pull a rebased branch ignoring the local state
```git
git fetch
git reset --hard origin/<branch>
```

## Show the last commit matching query string
```git
git show :/query
```

## Show branches containing given SHA
```git
git branch --contains <SHA>
```

## Temporarily ignore file changes
```git
git update-index --assume-unchanged <file>
```

## One-commit feature branch workflow
```git
git fetch --all -p
git checkout origin/master
git commit -m’changes’
git push origin HEAD:refs/heads/the-feature
```

## Changing author info in the repository history
```git
git filter-branch --env-filter '
OLD_EMAIL="old@example.com"
CORRECT_NAME="Marek Grzybek"
CORRECT_EMAIL="new@example.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags

git push --force --tags origin 'refs/heads/*'
```

___
# Links
* [http://ndpsoftware.com/git-cheatsheet.html](http://ndpsoftware.com/git-cheatsheet.html#loc=workspace;)
