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
