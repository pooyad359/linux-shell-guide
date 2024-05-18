# Environment Variables

This section covers commands related to environment variables.

## `env`

By running `env` in the terminal you will get a list of environment variables.

```bash
env
```

It can also be used to run a program with a set of environment variables:

```bash
env VAR1=val1 VAR2=val2 <command>
```

To run a program without a specific environment variable use `-u` flag:

```bash
env -u VAR1 <command>
```

## `export`

It can be used to set a new environment variable.

```bash
export VAR=value
```

It can also be used to remove an environment variable, using a `-n` flag:

```bash
export -n VAR
```

One common use case of `export` is to append a path to `PATH` environment variable:

```bash
export PATH=$PATH:<new path>
```

## `unset`

It can be used to remove environment variables:

```bash
unset VAR
```

## `source`

It evaluates content of a file. One use case is to set environment variables from a file where they are stored:

```bash
# file.sh
export VAR1=value1
export VAR2=value2
```

```bash
source file.sh
```

In this case `source` will set the variables in the environment.
However, often the environment variables for a project are stored in `.env` file in the following format:

```bash
# .env
VAR1=value1
VAR2=value2
```

This type of file can be used with `source` but first the default behavior of `source` must be changed, using `set -o allexport`:

```bash
set -o allexport
source .env
set +o allexport
```

Use `set +o allexport` to change the behavior of `source` to its original form.

## Alias

To create a alias for a command follow the pattern below:

```bash
alias new_command='command -args'
```

Example for making a list all files alias: `alias la='ls -la'`

Just typing `alias` will show you a list of existing aliases.
To make an alias persistent, you can add the definition to `~/.bashrc` and run `source ~/.bashrc` to execute the changes.
