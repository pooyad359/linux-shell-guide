# Linux CLI tutorial

## Linux version

## Using `uname`

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
