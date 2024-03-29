# Process Management

## Basics

Run a process in the background by adding `&` to the end of the line.

```bash
sh ./script.sh &
```

To see the list of running background jobs, use `jobs`, and to bring them to the foreground use `fg`. To send it to the background first we need to stop the processes by pressing `ctrl + Z` and then enter `bg` in the terminal. If there are multiple jobs, we can specify the job number: `$ fg %2`.

If we separate two commands by `&`, the first one will run in the background and the second one in the foreground. In other words, the commands will run asynchronously.

`&&`: When used between two commands, the second command will only be executed if the first one succeeds.
`||`: When used between two commands, the second command will only be executed if the first one fails.

Use `ps` to list processes. To see all the running processes use `ps -Al`.

## Terminate a Process

- `kill`: Terminate a process using id. `$ kill 8722`
- `kill -KILL`: Force kill a process
- `kill -l`: Lists all options for killing a process

## List Processes

Use command `ps` to see a list of running processes. By default it only shows the processes run by the user. To see all the processes use `ps ax` for short description of processes or `ps axww` for full description.

### Examples

- Search for a process by name (e.g., `python`): `ps axww | grep python`
- Search for a process by name and get PIDs: `ps -axww | grep python | cut -f 1 -d ' '` or `ps -axww | grep python | awk '{print $1}'`

Another way to find processes is using `pgrep`. It's a command like `grep` but it is used to find processes.

1. `pgrep firefox`: Get PIDs of "firefox" processes.
2. `pgrep -u username chrome`: PIDs of user's "chrome" processes.
3. `pgrep -x bash`: Get PID of "bash" if running.
4. `pgrep -f "python script.py"`: PIDs of "python script.py" processes.
5. `pgrep -c chrome`: Count running "chrome" processes.
6. `pgrep -d, -u username`: PIDs of user's processes, comma-separated.
7. `pgrep -l -x firefox`: List names and PIDs of "firefox" processes.

## Resource Usage

To see the list of top running processes and their resource usage, use `top`. It shows the list of processes and their resource usage in real-time. To exit `top` use `q`. Alternatively, we can use `htop` which is a more user-friendly version of `top`.

### Flags

- `-o COL`: To sort the table by COL. Some of the columns in the table you could sort by are `%MEM`, `%CPU`, `PID`, etc.

## End Processes

`kill` command kills a process by sending a signal. To see the list of signals available use `kill -l`.
It can be used without flag by passing PID of the process:

```bash
kill 8701 # PID
```

Signal name can be passed as flags, e.g., `kill -KILL <PID>`, and also signal number, e.g., `kill -9 <PID>`.
Most import signals are:

- `TERM` or `15`: It is the default value
- `KILL` or `9`: Forcefully terminate a process

Another command is `killall` which is similar to `kill` except it uses process name instead of PID. This is especially helpful if multiple instances of a program are running and we want to terminate all of them.

Another way to kill processes is using `pkill` which uses process name.

- `-f`: Match against the entire command line instead of just the process name.
- `-u`: Specify the user whose processes should be killed.
- `-P`: Send the signal to the parent process instead of the matching processes.
- `-x`: Only match processes whose names exactly match the pattern.

Here are a few examples of using `pkill`:

- `pkill firefox`: Terminates all processes with the name "firefox."
- `pkill -u username chrome`: Terminates all processes with the name "chrome" owned by "username."
- `pkill -f "python script.py"`: Terminates all processes that have "python script.py" in their command line.
- `pkill -x bash`: Terminates only processes with the exact name "bash."

## Background/Foreground Processes

We can send an application to background when we execute it by adding `&` to the end of execution command. E.g., `python app.py &`
We can also move a process to background by running it and then pressing `Ctrl`+`Z`. This will temporarily stop the process. We can then use `bg` to resume it in the background.

- `jobs`: Shows a list of processes we sent to background.
- `bg N`: Moves a process to background using the job number (`N`)
- `fg N`: Move a process to foreground using the job number (`N`)
- `kill %N`: Kill a process using job number. Refer to `kill` for the flags.

## Detached processes

Running a process in detached mode allows for a process to live when the terminal gets killed. One way to run a process in a detached mode is using `nohup` command.
Usage: `nohup <command> <arguments> &`
The `&` runs the process in the background.

Another way to run a process in detached mode is by disowning the process using `disown` command.
Example

```bash
./command &
disown # disown last command
```

```bash
$ ./command &
[1] 9876
$ disown 9876 # disown using pid
```

```bash
$ ./command &
[1] 9876
$ disown %1 # disown using job id
```

## Process Tree

`pstree` displays a tree-like representation of running processes on your system. It visually organizes the processes in a hierarchical manner, illustrating their parent-child relationships.

## Process ID

Every process has a unique ID called PID. We can use `ps` command to see the list of running processes and their PIDs. We can also use `pidof` command to get the PID of a process by its name.

Examples:

- `pidof python`: Get PID of "python" process.
- `pidof -s python`: Get PID of "python" process, single PID.
- `pidof -x python`: Get PID of "python" process, exact match.
- `pidof -x scrip.sh`: Get PID of "script.sh" process, exact match.

## Memory Usage

`free` command shows the amount of used and free system memory. It also shows the amount of memory used by the kernel and buffers.
Examples:

- `free`: Shows the amount of used and free system memory.
- `free -h`: Shows the amount of used and free system memory in human-readable format.
- `free -<SIZE>`: Shows the amount of used and free system memory. SIZE can be `b`, `k`, `m`, `g`, `B`, `K`, `M`, `G` for bytes, kilobytes, megabytes, and gigabytes respectively.
- `free -s <SECONDS>`: Shows the amount of used and free system memory every SECONDS seconds.
