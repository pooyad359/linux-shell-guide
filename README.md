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
This will move file `a.txt` and `b.txt` to the specified directory. Note the directory must exist.

- `-u`, `--update`: move only when the SOURCE file is newer than the destination file or when the destination file is missing
-  `-v`, `--verbose`: explain what is being done

## Delete/Remove
Use `rm` to delete files and `rmdir` to remove empty directories. If the directory is not empty, use `rm -r <dir name>` to 
recursively delete the content of the directory.
- `-f`: Force remove. Overrides the interactive mode and deletes the file(s) without confirmation.
