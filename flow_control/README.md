# Flow Control

## Table of Contents

- [IF statement](#if-statement)
  - [Operators](#operators)
  - [Boolean Operation](#boolean-operation)
- [Arrays](#arrays)
  - [Appending to an array](#appending-to-an-array)
  - [Deleting elements](#deleting-elements)
- [For Loops](#for-loops)
  - [Looping over array](#looping-over-array)
- [While Loops](#while-loops)
- [CASE](#case)
  - [Special operators](#special-operators)
- [Inline if statement](#inline-if-statement)
- [Functions](#functions)
  - [Scope](#scope)
  - [Return Values](#return-values)
  - [Arguments](#arguments)

## IF statement

Be mindful of space between characters when using if statement.

```bash
if [[ <expression> ]]
then
    <...>
elif [[ <expression> ]]
    <...>
else
    <...>
fi
```

Note the spaces in the if statement are critical.

### Operators

| Operators | Description                                       | Example         |
| --------- | ------------------------------------------------- | --------------- |
| !         | Not operator                                      | `! $a > 2`      |
| -n        | The length of STRING is greater than zero         | `-n $a`         |
| -z        | The length of STRING is zero (ie it is empty)     | `-z $a`         |
| =         | String equality                                   | `$a = "Hello"`  |
| !=        | String inequality                                 | `$a != "Hello"` |
| -eq       | Integer equality                                  | `$a -eq 2`      |
| -gt       | Integer greater than                              | `$a -gt 2`      |
| -lt       | Integer less than                                 | `$a -lt 2`      |
| -d        | path exists as directory                          | `-d $path`      |
| -e        | File exists                                       | `-e file.txt`   |
| -r        | File exists and read permission granted           | `-r file.txt`   |
| -s        | File exists and it's size is greater than zero    | `-s file.txt`   |
| -w        | File exists and the write permission is granted   | `-w file.txt`   |
| -x        | File exists and the execute permission is granted | `-x file.txt`   |

### Boolean Operation

Use `&&` for AND and `||` for OR operator:

```bash
if [[ -r $1 ]] && [[ -s $1 ]]
then
    echo Do something
fi
```

## Arrays

The simplest way to define an array is using `()`:

```bash
a=(1 2 3 4)
```

Or, you could assign values one by one:

```bash
a[0]=1
a[1]=2
```

An array can be printed using `echo ${array[@]}` or `echo ${array[*]}`:

### Appending to an array

```bash
a=(1 2 3)
a+=(4)
a+=(5 6)
```

### Deleting elements

Use `unset` to delete elements:

```bash
unset array[2]
```

## For Loops

The general syntax of a for-loop in linux is:

```bash
for item in list
do
    commands
done
```

Example:

```bash
for i in 1 2 3 4 5
do
    echo $i
done
```

To loop over a sequence of integers, you could use {a..b} pattern which prints all the integers from `a` to `b` (inclusive), or {a..b..c} which prints all the integers from `a` to `b` taking steps of size `c` (E.g., {0..10..2} returns even numbers from 0 to 10).

### Looping over array

Looping over an array is similar to printing an array:

```bash
for i in ${array[@]}; do
    echo $i
done
```

To loop over index of array (instead of values), use `!` before the array name:

```bash
array=(a b c)
for i in ${!array[@]}; do
    echo $i
done
```

Returns:

```console
0
1
2
```

## While Loops

The syntax of a while loop is:

```bash
while <condition>
do
    commands
done
```

You can use `break` and `continue` to break out of the loop or skip the rest of the commands in the loop. You can use `While true` to create an infinite loop.

## CASE

```bash
case <variable> in
    <pattern 1>)
        <...>
        ;;
    <pattern 2>)
        <...>
        ;;
esac
```

### Special operators

- `|`: To combine multiple patterns and execute the code if one of them is a match.
- `*`: Matches everything. similar to `*` in regex.
  Example:

```bash
case $1 in
    0|1)
        echo "It is 0 or 1"
        ;;
    2)
        echo "It is 2"
        ;;
    [3-9])
        echo "It is 3 to 9"
        ;;
    *)
        echo "Not a digit"
        ;;
esac

```

## Inline if statement

```bash
[[ 2 -gt 1 ]] && echo true || echo false
```

## Functions

Functions can be defined in two ways:

```bash
# Method 1
function my-func {
    commands
}

# Method 2
my-func () {
    commands
}

# Call the function
my-func
```

### Scope

Functions have access to global variables and can overwrite them. To avoid overwriting, you can specify that a variable is local using `local` keyword.

```bash
function my-func {
    local var1=1
}

```

If we don't use `local` keyword, then the variable is global (even if not defined before). We can use this property to set variables globally, or return values.

```bash
function my-func {
    var1=1
}

my-func
echo ${var1}
```

### Return Values

Functions can return values. The returned value is used for status check of the function. If it runs successfully, it should return 0, otherwise, an integer from 1 to 255. You can use `$?` right after calling the function to check it's status.

```bash
function my-func {
    local var1=1
    return 0
}

my-func
echo $?
```

### Arguments

To pass arguments to a function we can just add them after function name, separated by space.

```bash
my-func a b c d
```

The arguments could be accessed via index variables (`$1`, `$2`, etc.). Some of other variables are:

- `$#`: Number of arguments
- `$0`: Name of the function
- `$*`, `$@`: All the arguments passed to the function
  - Using `"$*"` returns a single string with all variables (space separated). E.g., `"$1 $2 ... $n"`.
  - Using `"$@"` returns a multiple strings for each variable (space separated). E.g., `"$1" "$2" ... "$n"`.
  - In other cases `$*` and `$@` behave similarly.
