# System

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

## Package Manager

- **Search**: `apt-cache search <name/phrase>`
- **Install**: `apt-get install <package>`

## `uptime`

The uptime command is used to display the current time, system's uptime, and the average load on the system over a period of time.

```bash
uptime
   15:32:47 up 2 days, 3:20, 3 users, load average: 0.45, 0.28, 0.19
```

- `15:32:47`: The current time of the system when the uptime command was executed.
- `up 2 days, 3:20`: The time since the system was last rebooted. In this example, the system has been running for 2 days and 3 hours and 20 minutes.
- `3 users`: The number of currently logged-in users on the system.
- `load average: 0.45, 0.28, 0.19`: The average load on the system over the last 1, 5, and 15 minutes, respectively. The load average represents the number of processes that are either in a running state or waiting for CPU time.

**Use the flag `--pretty` to get only the duration**

## `set`

It is used to view or modify various shell and environment variables within the current shell session.

- `-e`: Enables the "exit on error" option. If any command in a script returns a non-zero exit status, the script will terminate immediately
- `-x`: Enables the "debug mode" or "trace mode." When this option is set, the shell will print each command before executing it, along with the values of variables.
- `-v`:  Enables the "verbose" option. The shell will print each command before executing it (it will not print the expanded values of variables).
- `-u`: Enables the "treat unset variables as an error" option. If a variable is referenced but not set, the script will terminate with an error.

**Each of these flags can be disabled using their `+` variation, e.g., `+x` flag to disable debug mode.**

## Signal Handling

`trap` is used to set up signal handlers, allowing you to define actions that should be taken when the shell receives specific signals.
Usage: `trap '<command>' <SIGNAL>`
To remove a trap, just set the action/command to nothing: `trap "" <SIGNAL>`

- `-l`: List available signals
- `-p`: List active traps
