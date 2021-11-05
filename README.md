# Linux CLI tutorial
## Linux version
```
$ uname -a
  Linux DESKTOP-0D7PNN6 5.4.72-microsoft-standard-WSL2 #1 SMP Wed Oct 28 23:40:43 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```

## Pause/Sleep
sleeps for number of seconds enered

```sleep <seconds>```

## List Files
Use `ls` to list files. Options:
- `-a` or `--all`: Includes hidden files
- `-l`: Includes size and execution permission

## File type
Using `file` returns the type of the file based on its content (not extension)
Example:

```
$ file key.pem
  key.pem: PEM RSA private key
```

## View Text Files
To view a text file in the command line, use `less`.

## Move/Rename
To move multiple files just list them in `mv` command:

```
$ mv a.txt b.txt <dir name>
```

## Piping
We can use `|` to pass the output of a command as input to the next command:
```
$ ls -la /etc | less
```


## String Operations
- `sort`
- `tail`: `tail -n 2`, `tail -n +2`, `tail -n -2`
This will move file `a.txt` and `b.txt` to the specified directory. Note the directory must exist.

- `-u`, `--update`: move only when the SOURCE file is newer than the destination file or when the destination file is missing
-  `-v`, `--verbose`: explain what is being done

## Delete/Remove
Use `rm` to delete files and `rmdir` to remove empty directories. If the directory is not empty, use `rm -r <dir name>` to 
recursively delete the content of the directory.
- `-f`: Force remove. Overrides the interactive mode and deletes the file(s) without confirmation.


## Standard I/O
To redirect the content of a command to a file we can use `>`:
```
$ ls -a > output.txt
```
But if an error occurs the error would be returned in the console and the file would be empty. To redirect the error we could use `2>`. This will redirect the error messages to a file.
```
$ ls -a > output.txt 2> error.log
```
Linux file descriptors:
- Standarnd Input (`0`): `stdin`
- Standarnd Output (`1`): `stdout`
- Standarnd error (`2`): `stderr`

To redirect the errors to somewhere we don't care about we could use `/dev/null`. E.g.,
```
$ ls -a > output.txt 2> /dev/null
```

If we want to redirect the errors to the same file as well, we could use `2>&1`, which redirects `stderr` to `stdout`:
```
$ ls -a > output.txt 2>&1
```
Another way of doing the same thing is using `&>`:
```
$ ls -a &> output.txt
```

## Tee
To output something to `stdout` as well as to a file. E.g,
```
$ ls /etc | tee output.txt
```
To append to a file use flag `-a`:
```
$ ls /etc | tee -a output.txt
```
To output `stderr` to file as well use `2>&1` before pipe:
```
$ ls /etc 2>&1 | tee -a output.txt
```

## File Permission
`chmod` is used to set permission to a file or a directory. There are three types of permissions:
- Read: `r` has a value of 4
- Write: `w` has a value of 2
- Execute: `x` has a value of 1

The permission value is a sum of the value of permissions mentioned above. E.g, permission to read (4) and execute (1) will have a value of 5. 

The permissions are assigned to three groups:
- Owner
- Same group as owner
- Others

```
$ chmod 750 file
```
In the example above the owner will have the permission to read/write/execute, the other users in the same group will have the permission to read/execute, and others won't have permission to access the file.

An alternative way is to add/substract permission:
- User: `u`
- Group: `g`
- Others: `o`
- All: `a`

E.g., to add execution permission to group, use `g+x`, or to remove write/execute permission from others use `o-wx`.

## Processes
Run a process in the background by adding `&` to the end of the line.
```
$ sh ./script.sh &
```

To see the list of running background jobs, use `jobs`, and to bring them to the foreground use `fg`. To send it to the background first we need to stop the processes by pressing `ctrl + Z` and then enter `bg` in the terminal. If there are multiple jobs, we can specify the job number: `$ fg %2`.

If we separate two commands by `&`, the first one will run in the background and the second one in the foreground. In other words, the commands will run asynchronously.

`&&`: When used between two commands, the second command will only be executed if the first one succeeds.
`||`: When used between two commands, the second command will only be executed if the first one fails.

Use `ps` to list processes. To see all the running processes use `ps -Al`.
### Terminate Process
- `kill`: Terminate a process using id. `$ kill 8722`
- `kill -KILL`: Force kill a process
- `kill -l`: Lists all options for killinga process
- 
## Package Manager
- __Search__: `apt-cache search <name/phrase>`
- __Install__: `apt-get install <package>`

## TMUX
`sudo apt-get install tmux`
- Start: `tmux`
- Exit: (1) `ctrl + b` (2) press `x`, (3) press `y`
- Dettach: `ctrl +b` -> `d`
- Start a named session: `tmux new -s <name>`
- List of running sessions: `tmux ls`
- Split the window horizontally: `ctrl +b` -> `%`
- Split the window vertically: `ctrl +b` -> `"`
- Rename the window: `ctrl +b` -> `,`
- Go to next pane: `ctrl +b` -> `o`
- Toggle between two panes: `ctrl +b` -> `;`
- Switch window: `ctrl +b` -> `<window number>`
- Select window: `ctrl +b` -> `w`
- Re-attach a session: `tmux attach-session -t <name>`


## Arithmatic
Let `x=2` and `y=3`. To calculate the sum of two variables we could use ``echo $((x+y))``
Other operations supported: `+`, `-`, `*`, `/`, `%`. Note `/` is integer division and returns an integer.

## User Input
To get input from user, we could use `read`. To pass a prompt message we could use the flag `-p`:
```
$ read -p "Enter a number: " input
```

## If statements
```
if [ "$<variable>" = "<value>" ]
then
    <commands>
else
    <commands>
fi
```
Note the spaces in the if statement are critical.


## File size
Command `du` can be used to estimate disk usage of files and directories.
important flags:
- `-B`, `--block-size=SIZE`: To specify the block size returned. E.g., `-BM` returns the sizes in megabytes. Units are K,M,G,T,P,E,Z,Y.
- `-c`: Produces grand total
- `-d`, `--max-depth=N`: print the total for a directory on if it is N or fewer levels below.
- `-h`: Human readable
- `-m`, `-k`: to view the sizes in megabyts or kilobytes. Same as using `-BM` or `-BK`
- `-X`, `--exclude-form=FILE`: excludes file that match pattern stored in `FILE`
- `--exclude=PATTERN`: exlude files that match `PATTERN`


# TODO
- [ ] `ln`
- [ ] `grep`
- [ ] `df`
