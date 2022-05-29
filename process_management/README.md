# Process Management

## List Processes

Use command `ps` to see a list of running processes. By default it only shows the processes run by the user. To see all the processes use `ps ax` for short discription of processes or `ps axww` for full discription.

### Examples

- Search for a process by name (e.g., `python`): `ps axww | grep python`
- Search for a process by name and get PIDs: `ps -axww | grep python | cut -f 1 -d ' '` or `ps -axww | grep python | awk '{print $1}'`

## Resource Usage

To see the list of top running processes and their resource usage, use `top`.

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

## Background/Foreground Processes

We can send an application to background when we execute it by adding `&` to the end of execution command. E.g., `python app.py &`
We can also move a process to background by running it and then pressing `Ctrl`+`Z`. This will temporarily stop the process. We can then use `bg` to resume it in the background.

- `jobs`: Shows a list of processes we sent to background.
- `bg N`: Moves a process to background using the job number (`N`)
- `fg N`: Move a process to foreground using the job number (`N`)
- `kill %N`: Kill a process using job number. Refer to `kill` for the flags.

## TODO

- [ ] `top`
- [ ] `pidof`
- [ ] `nice`
- [ ] `renice`
- [ ] `df`
- [ ] `free`