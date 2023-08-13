# Basics of Using CLI

## Shortkeys

- `Ctrl` + `w`: Delete the last word
- `Ctrl` + `u`: Delete the entrie line
- `Ctrl` + `r`: search command line history
- `Alt` + `f`/`b`: Move forward/backward a word at a time
- `Ctrl` + `a`/`e`: Move to beginning and end of line
- `Ctrl` + `k`: delete (kill) from cursor to the end of line
- `Alt` + `#` (`Alt` + `Shft` + `3`): Turn the command into a comment by adding `#`
- `Ctrl` + `l`: Clear the screen

## Command Line History

- `history`: get the command history
- `!n`: execute nth command in history
- `!!`: last command
- `!$`: last argument
- `!-n`: execute nth command before current (e.g., !-1 last command)
- `!string`: execute last command starting with `string`
- `!?string`: execute last command containing `string`

## Piping

We can use `|` to pass the output of a command as input to the next command:

```bash
ls -la /etc | less
```

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

- Standard Input (`0`): `stdin`
- Standard Output (`1`): `stdout`
- Standard error (`2`): `stderr`

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

## User Input

To get input from user, we could use `read`. To pass a prompt message we could use the flag `-p`:

```bash
read -p "Enter a number: " input
```

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
