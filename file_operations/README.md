# File Operations

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

## Move/Rename

To move multiple files just list them in `mv` command:

```bash
mv a.txt b.txt <dir name>
```

## Delete/Remove

Use `rm` to delete files and `rmdir` to remove empty directories. If the directory is not empty, use `rm -r <dir name>` to
recursively delete the content of the directory.

- `-f`: Force remove. Overrides the interactive mode and deletes the file(s) without confirmation.

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

## Links

Links are shortcuts to files or directories. To create a link you can use `ln` command.

### Hard Link

Creates a link to a file, which is treated as a second file that has a content insync with the original file. Essentially, both files will be pointing to the same place on disk. Therefore, even if the original file is deleted, the hard link will still work normally.
`ln <original> <link_name>`

### Soft Link

The soft link points at the original file, and it can be treated in most ways like a hard link. But, if the original file is deleted, the link will not work anymore.
Use `-s` flag in `ln` to specify it is a soft link (a.k.a. symbolic link).

### `readlink`

It can be used to disclose the file that a symbolic link points to.

## Program Info

- `which <program>`: Full path to the command/program.
- `whereis <program>`: All existing paths for the program including `man` page.
- `whatis <program>`: Short description of a command/program.
- `man <program>`: Manual page for the command/program.

## File Path

### `basename`

Returns the file name:

```bash
file=/home/user/file.txt
basename $file # file.txt
```

### `dirname`

removes the file name from a path, i.e., returns the name of the directory:

```bash
file=/home/user/file.txt
dirname $file # /home/user
```

## Create Temporary File

`mktemp` creates a temporary file and returns its path.

```bash
mktemp
# /tmp/tmp.VpWN5xysbv
```
