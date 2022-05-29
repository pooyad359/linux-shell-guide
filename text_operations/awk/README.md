# `awk`

It's a programming language for working with files. General usage is `awk [options] [program] [file]`.

## Flags

- `-F fs`: To change field separator to `fs`.
- `-f file`: Read awk script from `file`.
- `-v var=value`: Allows to set a variable so it can be used in awk script.
- `-mf N`: Maximum number of fields to be processed.
- `-mr N`: Maximum record size.

## Filtering by column

`print` function in `awk` allows user to return a value. Using `$0` returns the entire file, and `$N` returns the Nth field. By default, it assumes the file is space-separated.

Return the first and fourth column:

```bash
awk '{print $1 $4}'
```

The output will also be space-sparated.
To change the field separator use `-F` flag.
Column number can be a variable:

```bash
NF=9
awk '{print $(NF)}'
```

## Replacing values

You can replace a value in the lines, by replacing the value of a field and then returning the whole line:

```bash
awk '{$4="Hello";print $0}'
```

## Adding text to the output

```bash
awk '{print $1 " ---> " $2}'
```

## Pre/Post scripts

To execute `awk` script before or after the main script, you can use `BEGIN` and `END` keywords:

```bash
awk 'BEGIN {print "FILE HEADER"}
>{print $0}
>END {print "---END---"}
'
```

## Built-in variables

There are variables that are used in `awk` and by changing them you can customize it's behaviour.

- `FS`: field separator
- `FIELDWIDTHS`: a space separated list of numbers, which can be used for fixed-width fields.
- `RS`: Record separator character.
- `OFS`: Field separator in the output.
- `ORS`: Record separator in the output.
- `ARGC`: Number of command line arguments.
- `ARGV`: Array of command line arguments.
- `ARGIND`: Index of current file in `ARGV`.
- `ENVIRON`: Array of environment variables. Can be accessed via variable name: `'{print ENVIRON["HOME"]}'`
- `FILENAME`: Name of the input file.
- `FNR`: Number of current record in the data file.
- `NF`: Total number of fields in the current record.
- `NR`: Total number of processed records.

```bash
awk 'BEGIN{FS=",";OFS="\t"} {print $1, $2}'
```

## Conditional operation

You can use if statement in `awk` code:

```bash
awk '{if ($1 > 20) print $1}'
```

or if-else:

```bash
awk '{if ($1 > 20) print $1; else print 0}'
```

## For-loop

```bash
awk '{
    total =0
    for (i=1;i<4;i++)
    {
        total += $i
    }
    print "Total:", total
}'
```

## Math functions

Some of the math functions available in `awk`:

- `cos`
- `sin`
- `exp`
- `int`
- `log`
- `rand`
- `sqrt`

## String functions

- `length(STRING)`: Number of characters in a string
- `index(STRING, CHAR)`: Returns the index of `CHAR` in `STRING` starting from `1`. Returns `0` if not found.
- `gsub(PATTERN, REPLACE)`: Regex match and replace. Example, convert `.py` to `.js`: `ls | awk '{ gsub(/.py/, ".js"); print }'`
- `sub(PATTERN, REPLACE, variable)`: Regex match and replace. Uses `variable` as input and saves the results inplace. Example, convert `.py` to `.js`: `ls | awk '{ sub(/.py/, ".js", $0); print $0 }'`
- `match(STRING, PATTERN)`: Returns the index of the first match.
- `split(STRING, output-array, SEPARATOR, separator-array)`: Splits the string into elements using the separator. The output array is saved in the second argument, and the separators in the separators. Example, remove file extensions: `ls | awk '{split($0, a, ".", seps); print a[1]; }'`.
- `printf`: Allows printing using a C-like formatting.
- `sprintf(TEMPLATE, value)`: Formats string similar to `printf` but the result is returned to a variable and not stdout.
- `strtonum(STRING)`: Returns the numeric value of a string. If not a number, it will return `0`.
- `substr(STRING, START, [END])`: Returns a substring.
- `tolower(STRING)`: To lower case.
- `toupper(STRING)`: To upper case.

## Custom Functions

You can define your own functions:

```bash
awk '
function myfunc(x){
    return sprintf("<<< %s >>>",x)
}
{print myfunc($0)}
'
```
