# System

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

__Use the flag `--pretty` to get only the duration__

## `set`

It is used to view or modify various shell and environment variables within the current shell session.

- `-e`: Enables the "exit on error" option. If any command in a script returns a non-zero exit status, the script will terminate immediately
- `-x`: Enables the "debug mode" or "trace mode." When this option is set, the shell will print each command before executing it, along with the values of variables.
- `-v`:  Enables the "verbose" option. The shell will print each command before executing it (it will not print the expanded values of variables).
- `-u`: Enables the "treat unset variables as an error" option. If a variable is referenced but not set, the script will terminate with an error.

__Each of these flags can be disabled using their `+` variation, e.g., `+x` flag to disable debug mode.__

## Signal Handling

`trap` is used to set up signal handlers, allowing you to define actions that should be taken when the shell receives specific signals.
Usage: `trap '<command>' <SIGNAL>`
To remove a trap, just set the action/command to nothing: `trap "" <SIGNAL>`

- `-l`: List available signals
- `-p`: List active traps
