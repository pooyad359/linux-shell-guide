# Concurrency

Some tasks could benefit from concurrency either through multi-processing or multi-threading. This can be achieved in a number of ways.

## Background Jobs

We can send a program to background using `&`. Any process executed afterwards will run concurrently.

```bash
program1 & program2
```

This will execute `program1` and send it to background and immediately starts executing `program2`.

```bash
sleep 1 &
sleep 1 &
```

This program will take about 1 second to run, since the second line starts immediately after the first and will finish (almost) together. Same thing can be achieved using a loop:

```bash
for i in `seq 10`;do
    sleep 1 &
done
```

You can also run two jobs concurrently and wait for both to finish before executing the next command:

```bash
echo $(sleep 1 & sleep 2); echo finished
```

A better way to assure completion of a process is using [`wait`](#wait) command.

## `xargs`

It is a useful command to pipe the input arguments into a command, and run them as independent processes.
General usage is:

```bash
<arguments_source> | xargs <command>
```

Example:

```bash
# One way to remove all the files in the current directory
ls | xargs rm
```

### `xargs` Flags

- `-P`: Maximum number of concurrent processes
- `-0` or `--null`: Items are separated by a null, not whitespace.
- `d CHAR`: Set `CHAR` as item delimiter.

## `parallel`

Run commands on multiple processors. It can be used in two ways:

1. It will run the command for each of arguments in a separate process.

    ```bash
    parallel <command> ::: arg1 arg2 arg3
    ```

2. Works similar to `xargs`:

    ```bash
    <argument_source> | parallel <command>
    ```

Example:
Compress all `.jpg` files using `gzip`.

```bash
ls *.jpg | parallel gzip
```

### `parallel` flags

- `-a FILE`: Read arguments from `FILE`
- `--bar`: Show progress bar
- `--eta`: Show estimated time in seconds
- `-j N` or `--jobs N`: Parallelize across `N` processors. `0` means as many as possible. Default is one job per CPU core on each machine.
  - `+N`: Add `N` to number of CPU cores and use as number of parallel jobs.
  - `-N`: Subtract `N` to number of CPU cores and use as number of parallel jobs.
  - `N%`: Use `N` percent of CPU cores to run the jobs.
- `-k`: Keep the order of the input. By default the output is returned as soon as job is finished.
- `--file`: The output of each job is saved to a file, and file's name is printed.
- `--progress`: Sow progress of the job.
- `--number-of-cpus`: Prints the number of CPUs
- `--number-of-cores`: Prints the number of CPU cores

### `parallel` special characters

Special characters can be used to manipulate input arguments before passing them into the program. For instance, in the following code `{}`, passes input line into the program:

```bash
<args> | parallel <program> {}
```

Other special characters include:

- `{.}`: Input line without extension (to remove file extension form file name or path).
- `{/}`: Basename of the input line (excluding the path information).
- `{/.}`: Basename of the input line without extension.
- `{//}`: Dirname of the input line (excluding the file's name).
- `{#}`: Sequence number of job (starting from 1).
- `{%}`: Slot number of job (starting from 1), i.e., which cpu core the job is running on.
- `{N}`: `N`th argument from input line. If `N` is negative, it refers to `N`th last argument. It can be used with `/`, `/.`, `//`, etc. to manipulate paths. E.g., `{2/.}` to get base name without the extension from second argument on each line.

## `wait`

Wait for a process to complete. If it is used without any arguments, waits for all the processes to finish.
It also accepts `PID` and waits for that specific process to finish.

```bash
<command> &
JOB=${!} # get PID of the job
<other commands>
wait $JOB
```
