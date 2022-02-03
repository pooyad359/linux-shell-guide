# Git

## File Operation

- `git ls-files`: Lists the tracked files.
- `git rm <file>`: Deletes an unstaged file, and add the change to staged area.
- `git rm --cached <file>`: Removes a file from being tracked.
- `git mv <file> <new_name>`: Rename/Move file, and add the change to staged area.

## History

- `git log`: See commit history.
- `git log <file>`: See commit history that contains `file`.
- `-N`, `-n N`, `--max-count=N`: To show the last `N` commits.
- `--oneline`: History with short (one line) description.

## Discard Changes

### Unstaged Changes

- `git checkout <file>`: To remove/undo uncommitted changes in a tracked file
- `git checkout .`: Undo uncommited changes to all tracked files.
- `git restore`: Same as `git checkout`

### Untracked Files

- `git clean -d`: To delete untracked files.
- `git clean -dn`: Just lists the files that would be deleted.
- `git cleand -df`: Forcefully deletes files

### Staged Changes

To undo the changes to a staged files, first the files need to be unstaged, then, one of the methods above can be used to undo the changes.

- `git reset <file>`: To unstage a file
- `git restore --staged <file>`: To unstage a file

### Commited Changes

- `git reset --soft HEAD~n`: Undo the last `n` commits. Keeps the changes made in the commits staged.
- `git reset --hard HEAD~n`: Undo the last `n` commits. Discards all the changes.

## Stashing

- `git stash`: Saves the unstages changes.
- `git stash list`: List of saved stashes.
- `git stash apply n`: brings back the saved stash number `n`.
- `git stash pop n`: Removes stash `n` from list and adds it to project.
- `git stash drop n`: Discards stash `n`
- `git stash clear`: Removes all the stashes

## Reflog

- `git reflog`: Retursn a list of all the changes to HEAD, including resets.
- `git reset --hard <hash>`: We can use reflog hash here to go back to specific point.
- `git checkout <hash>`: To view code in detached mode.
  - `git checkout -b <branch>`: To move the checked out changes to another branch.
