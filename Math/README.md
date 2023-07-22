# Math

## `factor`

Prime factorization of a number:

```bash
factor 108 # 108: 2 2 3 3 3
```

## `bc`

An arbitrary precision calculator language.
Example:

```bash
echo '1+1' | bc # 2
bc <<< '1+1' # 2
```

Specify decimal places precision.

```bash
echo 'scale=5; 2/3' | bc # .66666
```

## `datamash`

`datamash` command is a tool for performing basic and advanced numeric, textual, and statistical operations on structured text data.
Usage: `datamash <OPTIONS> <OPERATIONS>`
Example:

```bash
# Sum numbers 1 to 10
seq 10 | datamash sum 1
# Perform sum operation over the first column of the data
```

You can also perform multiple operations at once.

```bash
seq 10 | datamash sum 1 mean 1 sstdev 1
```

### Operations Available

- Numeric Grouping operations: sum, min, max, absmin, absmax, range
- Textual/Numeric Grouping operations: count, first, last, rand, unique, collapse, countunique
- Statistical Grouping operations: mean, trimmean, median, q1, q3, iqr, perc, mode, antimode, pstdev, sstdev, pvar, svar, mad, madraw, pskew, sskew, pkurt, skurt, dpo, jarque, scov, pcov, spearson, ppearson

Flags:

- `-t`: To specify the delimiter. E.g., `-t ,` for operating on csv files
- `-g`: To perform groupby. Allows you to groupby a column and then perform operations. E.g. `datamash -g 1 mean 2`, which groups by first column and then returns the mean value of the second column for each group.
- `-h`: Prints a header line as the first line of the output.
- `-H`: Specifies that the first line should be treated as the header. This allows you to use column name instead of numbers for operations.
