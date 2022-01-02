# Linux CLI tutorial

## Linux version

```bash
uname -a
```

```console
  Linux DESKTOP-0D7PNN6 5.4.72-microsoft-standard-WSL2 #1 SMP Wed Oct 28 23:40:43 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```

## Pause/Sleep

sleeps for number of seconds enered

`sleep <seconds>`

## List Files

Use `ls` to list files. Options:

- `-a` or `--all`: Includes hidden files
- `-l`: Includes size and execution permission

## File type

Using `file` returns the type of the file based on its content (not extension)
Example:

```bash
file key.pem
```

```console
  key.pem: PEM RSA private key
```

## View Text Files

To view a text file in the command line, use `less`.

## Move/Rename

To move multiple files just list them in `mv` command:

```bash
mv a.txt b.txt <dir name>
```

## Piping

We can use `|` to pass the output of a command as input to the next command:

```bash
ls -la /etc | less
```

## String Operations

- `sort`
- `tail`: `tail -n 2`, `tail -n +2`, `tail -n -2`
  This will move file `a.txt` and `b.txt` to the specified directory. Note the directory must exist.

- `-u`, `--update`: move only when the SOURCE file is newer than the destination file or when the destination file is missing
- `-v`, `--verbose`: explain what is being done

## Delete/Remove

Use `rm` to delete files and `rmdir` to remove empty directories. If the directory is not empty, use `rm -r <dir name>` to
recursively delete the content of the directory.

- `-f`: Force remove. Overrides the interactive mode and deletes the file(s) without confirmation.

## Standard I/O

To redirect the content of a command to a file we can use `>`:

```bash
ls -a > output.txt
```

But if an error occurs the error would be returned in the console and the file would be empty. To redirect the error we could use `2>`. This will redirect the error messages to a file.

```bash
ls -a > output.txt 2> error.log
```

Linux file descriptors:

- Standarnd Input (`0`): `stdin`
- Standarnd Output (`1`): `stdout`
- Standarnd error (`2`): `stderr`

To redirect the errors to somewhere we don't care about we could use `/dev/null`. E.g.,

```bash
ls -a > output.txt 2> /dev/null
```

If we want to redirect the errors to the same file as well, we could use `2>&1`, which redirects `stderr` to `stdout`:

```bash
ls -a > output.txt 2>&1
```

Another way of doing the same thing is using `&>`:

```bash
ls -a &> output.txt
```

## Tee

To output something to `stdout` as well as to a file. E.g,

```bash
ls /etc | tee output.txt
```

To append to a file use flag `-a`:

```bash
ls /etc | tee -a output.txt
```

To output `stderr` to file as well use `2>&1` before pipe:

```bash
ls /etc 2>&1 | tee -a output.txt
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

```bash
chmod 750 file
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

```bash
sh ./script.sh &
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

## Package Manager

- **Search**: `apt-cache search <name/phrase>`
- **Install**: `apt-get install <package>`

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

Let `x=2` and `y=3`. To calculate the sum of two variables we could use `echo $((x+y))`
Other operations supported: `+`, `-`, `*`, `/`, `%`. Note `/` is integer division and returns an integer.

## User Input

To get input from user, we could use `read`. To pass a prompt message we could use the flag `-p`:

```bash
read -p "Enter a number: " input
```

## If statements

```bash
if [ "$<variable>" = "<value>" ]
then
    <commands>
else
    <commands>
fi
```

Note the spaces in the if statement are critical.

## File size (Disk Usage)

Command `du` can be used to estimate disk usage of files and directories.
important flags:

- `-B`, `--block-size=SIZE`: To specify the block size returned. E.g., `-BM` returns the sizes in megabytes. Units are K, M, G, T, P, E, Z, Y.
- `-c`: Produces grand total
- `-dN`, `--max-depth=N`: print the total for a directory on if it is `N` or fewer levels below.
- `-h`: Human readable
- `-m`, `-k`: to view the sizes in megabyts or kilobytes. Same as using `-BM` or `-BK`
- `-X`, `--exclude-form=FILE`: excludes file that match pattern stored in `FILE`
- `--exclude=PATTERN`: exlude files that match `PATTERN`

## File System

To see information about file system use `df` command.

**flags:**

- `-h`: Human readable
- `-BX`: To set block size, where `X` is the size flag (similar to `du` block size flags)

## Search for files

Command `find` can be used to search the disk for files or directories.
Usage: `find <path> <expression>`
Example:

```bash
find . -name '*.js'
```

Expressions can be in five forms:

- **Tests**: Return a true/false values which is used to filter results
- **Actions**: They run other operations (e.g., printing) and return true/false if operation was successful
- **Global Options**: Affect the operation of tests and actions
- **Positional Options**: Only affect test or action directly follow after them
- **Operators**: To join expressions. E.g., `-o` for logical OR and `-a` for logical AND. If missing `-a` is assumed.

### Important Global Option flags

- `-maxdepth LEVEL`: Maximum levels from the entered path to search for the pattern. E.g, `find . -maxdepth 2 -name '*.py'`
- `-mindepth LEVEL`: Minimum levels from the entered path to search for the pattern. E.g, `find . -mindepth 2 -name '*.py'`

### Important flags for Test Expressions

- `-name PATTERN`: match filename to the pattern (`-iname` for case insensitive)
- `-empty`: file/directory is empty
- `-executable`: match files which are executable
- `-path PATTERN`: match file path to the pattern (`-ipath` for case insensitive)
- `-regex PATTERN`: match file path to the regex pattern (`iregex` for case insensitive)
- `-size N[ckMG]`: Check the file size is exactly N (numbers are rounded up). Use +N to match files larger than N, and -N for files smaller than N. Block size can be `c` for character/byte, `k` for kilobytes, `M` for Megabytes, and `G` for Gigabytes.
- `-type TYPE`: Matches the file type. The supported file types are:
  - `d`: directory
  - `f`: regular file
  - `l`: symbolic link
  - `s`: socket
- `-mmin N`: File was modified N minutes ago. Use -/+ for less/more.
- `-mtime N`: File was modified N days ago. Use -/+ for less/more.

### Important flags for Action Expressions

- `-delete`: Delete files
- `-exec COMMAND \;`: Executes COMMAND for each file. `{}` can be used to pass the file path as argument to the command. E.g., `find . -name '*.exe' -exec echo {} \;`
- `-execdir COMMAND \;`: Executes COMMAND from the subdirectory of the matched file. Use `{}` for file path.
- `-print`: prints the file path
- `-print0`: Same as print, but the results will be concatenated in a single line.

### Operators

- `-a`, `-and`: AND operator for expressions. `find . -name '*.jsx' -and -name '*.js'`. If no operator is used it will assume and operator.
- `-o`, `-or`: OR operator for expressions.
- `-not`, `!`: NOT operator. `find . ! -name '*.jsx'`
  **`()` can be used to enforce precedence, but they should be used as `\(` and `\)`**

## History

To view a history of used commands, you can use `history`.
Using the line number in history, you could execute the command again:

```bash
!128 # This will run command 128 from history
```

### Flags

- `-c`: Clear history
- `-dN`: Clear command number `N` in history

### Examples

- Get last 10 commands: `history | tail -n 10`
- Search for a command using a keyword (e.g., `docker`): `history | grep docker`

## Alias

To create a alias for a command follow the pattern below:

```bash
alias new_command='command -args'
```

Example for making a list all files alias: `alias la='ls -la'`

Just typing `alias` will show you a list of existing aliases.
To make an alias persistent, you can add the definition to `~/.bashrc` and run `source ~/.bashrc` to execute the changes.

## XARGS

Converts stdout into arguments for a command. Let's say command1 generates output in stdout and we want to use it as input for command2 (which doesn't accept arguments from stdout). Then we could leverage `xargs`:

```bash
command1 | xargs command2
```

Examples:

- Remove a list of file that are stored in another file: `cat files_to_delete.txt | xargs rm`
- View detailed list of all files larger than 10 MB: `find . -size +10M | xargs ls -l`

## TODO

- [ ] `ln`
- [ ] `nohup`
- [ ] `dd`
- [ ] functions
- [ ] Loops
- [ ] `pr`
