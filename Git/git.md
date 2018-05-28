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
