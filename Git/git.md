## Revert file to specific commit

git checkout commit_id -- file1/to/restore file2/to/restore

## Reset commit

git reset HEAD~

## Reset index

git reset

## Ignore folder / directory

directory_name/

## Amend a git commit message

git commit --amend -m "New commit message"

## Revert git to commit id

git reset --hard f414f31
git reset --soft HEAD@{1}
git commit -m "Reverting to the state of the project at f414f31"

## Clean up your local branches after merge and delete in GitHub

1. List branches in local machine
   The command `git branch -a` shows the test branch feature-collaboration is present on local and also present on remote
1. Prune/Cleanup the local references to remote branch

- The command `git remote prune origin --dry-run` lists branches that can be deleted/pruned on your local. An option `--dry-run` is needed.

- Now go ahead and actually prune/cleanup the local references by running the command `git remote prune origin`. Note that you don't need an option `--dry-run`.
- Again, run the command `git branch -a` will show the local status of branches.

1. Delete local branch
