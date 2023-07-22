# Script Arguments

Most commands in linux accept arguments and flags. You might want to do the same for your script or function.

## Input arguments

You can find the number of input arguments using `$#`, and access them through indexing `$<index>`. E.g. `$1`, `$2`, `$3`,  would access the first,second, and third argument. `$0` would access the script path (depending on how it was called it could be just file's name or a relative path). For functions, `$0` would access the shell used to run the function (e.g., `/bin/bash`).
There is also `$@` which has access to an array of arguments.

```bash
# Print all the input arguments
for arg in $@; do
    echo "Argument: $arg"
done
```

## Using Flags

The easiest way to use flags is by combining `getopts`, while-loop, and case statement:

```bash
#!/bin/bash
while getopts 'abc' OPTION; do
  case "$OPTION" in 
    a) 
      echo "Option a"
      ;;

    b)
      echo "Option b"
      ;;

    c)
      echo "Option c"
      ;;

    ?) 
      # Other cases
      echo "Usage: $(basename $0) [-a] [-b] [-c]"
      exit 1
      ;;
  esac
done
```

Only the letters in the string after `getopts` are valid. Anything else would invoke `?` option.

- Adding `:` to the beginning of flags list, tells shell to not throw error if invalid flag is passed. E.g., `":abc"`
- Adding `:` after a flag means the flag expects an argument. E.g., `":ab:c"` means we need to pass some value after `-b`.
- If a flag is followed by a value, you can access the value in `$OPTARG`.

## Combining flags and arguments

Imagine the case where we want to process some file. We might have a few flags to define how we are going to process them, then at the end of the command we pass in a list of files. E.g., `process -a -f csv file1.csv file2.csv`. We can capture the flags and their values with `getopts`, but not the name of the files. Alternatively, we could use `$@`, but it would give us a list of all arguments, including the flags. To solve this issue we can use another command called `shift`. `shift` is followed by a number (`N`), which tells it to ignore the first `N` arguments when we use `$@`. The way we are going to use it is by adding it after the end of while loop: `shift $(($OPTIND -1))`.
What is `OPTIND`? It is the index of argument that is processed at that stage. When we add it after while loop, it's value would be the index of first non-flag argument (i.e., the first file name).
Therefore, by using `shift $(($OPTIND -1))`, we will ignore all the flags, which means `$@` will only contain non-flag arguments.

Example:

```bash
# script.sh
while getopts 'af:' OPTION; do
    case "$OPTION" in
    a)
        echo "Using flag -a"
        ;;
    f)
        VALUE=$OPTARG
        echo "Using flag -f with value $VALUE"
        ;;
    ?)
        echo "Invalid Argument"
        exit 1
        ;;
    esac
done
shift "$(($OPTIND - 1))"

for file in $@; do
    echo "FILE: $file"
done
```

```bash
bash script.sh -a -f csv file1.csv file2.csv
# Using flag -a
# Using flag -f with value csv
# FILE: file1.csv
# FILE: file2.csv
```

## Default values

To make sure a script always has input arguments use this pattern: `VAR=${1:<message>}`. If the first argument (`$1`) is empty the message will be displayed.
To set a variable with a default value, use this pattern: `VAR=${1:-VALUE}`. If the first argument (`$1`) is empty `VALUE` will be asigned to `VAR`.
