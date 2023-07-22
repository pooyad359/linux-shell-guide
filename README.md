# Linux CLI tutorial

## Linux version

### Using `uname`

```bash
uname
```

```console
Linux
```

To get release info use `-r` flag:

```bash
uname -r
```

```console
5.10.147+
```

, or use `-a` to get more detailed information:

```bash
uname -a
```

```console
  Linux 19ca26f221c6 5.10.147+ #1 SMP Sat Dec 10 16:00:40 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
```

### Using `/proc/version`

View the version information stored in `/proc/version`:

```bash
cat /proc/version
```

## Pause/Sleep

sleeps for number of seconds entered

`sleep <seconds>`

## Package Manager

- **Search**: `apt-cache search <name/phrase>`
- **Install**: `apt-get install <package>`

## Arithmetic

Let `x=2` and `y=3`. To calculate the sum of two variables we could use `echo $((x+y))`
Other operations supported: `+`, `-`, `*`, `/`, `%`. Note `/` is integer division and returns an integer.

## Shortkeys

- `Ctrl` + `w`: Delete the last word
- `Ctrl` + `u`: Delete the entrie line
- `Ctrl` + `r`: search command line history
- `Alt` + `f`/`b`: Move forward/backward a word at a time
- `Ctrl` + `a`/`e`: Move to beginning and end of line
- `Ctrl` + `k`: delete (kill) from cursor to the end of line
- `Alt` + `#` (`Alt` + `Shft` + `3`): Turn the command into a comment by adding `#`

## Command Line History

- `history`: get the command history
- `!n`: execute nth command in history
- `!!`: last command
- `!$`: last argument
- `!-n`: execute nth command before current (e.g., !-1 last command)
