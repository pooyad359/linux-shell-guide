# Flow Control

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
| -r        | File exists and read permission granted           | `-e file.txt`   |
| -s        | File exists and it's size is greater than zero    | `-e file.txt`   |
| -w        | File exists and the write permission is granted   | `-e file.txt`   |
| -x        | File exists and the execute permission is granted | `-e file.txt`   |

### Boolean Operation

Use `&&` for AND and `||` for OR operator:

```bash
if [[ -r $1 ]] && [[ -s $1 ]]
then
    echo Do something
fi
```

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

## TODO

- [ ] functions
- [ ] Loops
- [ ] inline if-statement
- [ ] test
