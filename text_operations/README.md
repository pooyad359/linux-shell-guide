# Text Operations

## Table of Contents

1. [`cat`](#cat)
2. [`diff`](#diff)
3. [`nl`](#nl)
4. [`wc`](#word-count-wc)
5. [`paste`](#paste)
6. [`join`](#join)
7. [`look`](#look)
8. [`grep`](#grep)
9. [`head` and `tail`](#head-and-tail)
10. [Remove columns (`colrm`)](#remove-columns-colrm)
11. [`cut`](#cut)
12. [Generate Sequences (`seq`)](#generate-sequence-seq)
13. [Sorting (`sort`)](#sorting-sort)
14. [Split files with (`split`)](#split-files-with-split)
15. [`tr`](#tr)
16. [`uniq`](#uniq)
17. [Random String Generation](#random-string-generation)

## `cat`

Print and concatenate files.
To concatenate multiple files into one: `cat file1 file2 > target`

### `cat` flags

- `-n`: Adds line number to the beginning of each line

---

## `diff`

Compare files line by line. In it's most basic usage (`diff file1 file2`), it lists all the changes to turn `file1` into `file2`.
__Flags:__

- `-y`, `--side-by-side`: Show the changes side-by-side
- `--unified`: Uses unified format to show changes (similar to `git diff`).
- `-q`, `--brief`: Just prints a line if the files are not the same.
- `-s`: Report when two files are the same.
- `-r`, `--recursive`: Recursively compare any subdirectories found.

### Useful examples of `diff`

- Show the list of files that differ in two directories:
  `diff -r -q dir1 dir2`

## `nl`

Add line number to text. It works similar to `cat -n`.

### `nl` flags

- `-pBRE`: Returns all the lines but only numbers the lines that match regular expression `BRE`. E.g., number lines that start with `import`: `nl -b p^def file.txt`
- `-sD`: Uses delimiter `D` between line number and the line. E.g., use `=` as delimiter: `nl -s= p^def file.txt`

---

## Word Count (`wc`)

Print newline, word, and byte counts for each FILE, and a total line if
more than one FILE is specified.

```bash
wc file.txt
```

```console
14  18 172 file.txt
```

### `wc` flags

- `-c`: return number of bytes
- `-l`: return number of lines
- `-w`: return number of words

---

## `paste`

Adds files together side-by-side, i.e., concatenate lines of each file together with a delimiter.

```bash
paste file1 file2
```

### `paste` flags

- `-d D`: To use `D` as delimiter. Default delimiter is tab.
- `-s`: paste one file at a time instead of in parallel, i.e., lines of each file will be concatenated into a single row.

### Examples for `paste`

- Turn a column of numbers into a single line separated by comma:
`cat file.txt | paste -sd ,`

- Calculate sum from a column of numbers:
`cat file.txt | paster -sd + | bc`

---

## `join`

Joins the content of two files similar to a left inner join operation in SQL. To do the operation properly, you should make sure the common field is sorted in both files. By default, it uses the first column of each file, using white space as field separator.

```bash
join file1 file2
```

__Flags:__

- `-t`: Specify the field separator. E.g., to use comma: `join -t ',' file1 file2`
- `-1`: Specify common field of first file. E.g., Use the third column of file1: `join -1 3 file1 file2`
- `-2`: Specify common field of second file. E.g., Use the third column of file2: `join -2 3 file1 file2`
- `-a FILENUM`: Print unpaired lines from a file. `FILENUM` is `1` or `2` to specify first or second file.
- `-e VAL`: Replace missing fields with `VAL`.

### Join two csv files

Imagine we have the following files:
`population.csv`:

```csv
Country,Population
China,1412600000
India,1375586000
USA,334233854
Indonesia,275773800
Pakistan,235825000
```

and
`area.csv`:

```csv
Country,Area
Russia,16378410
Canada,9984670
China,9596961
USA,9525067
India,3287263
```

We want to join the files on country name. First, we need to sort the files using `csvsort` then join them:

```bash
join --header -t ',' <(csvsort -c 1 population.csv ) <(csvsort -c 1 area.csv)
```

## `look`

Look for lines starting with a given prefix. Use `-f` for case insensitive search.

```bash
look def app.py # Finds
```

---

## `grep`

Search the content of a file. Simple example is `grep hello hello.txt`, which searches in file `hello.txt` and returns the lines with the word `hello`.

### `grep` flags

- `-i`: Case insensitive match
- `-v`: Invert search. Only returns lines where the match is not found.
- `-n`: Adds line number in the file to the output
- `-w`: Matches the whole words. E.g., `grep -w hi hello.txt` will match the occurrence of `hi` and not when it is part of another word like `hide`.
- `-r`: Searches recursively in all files in a directory. Default directory is `./`
- `-c`: Number of occurrence per file.
- `-E`: To search using extended regex pattern and return name of the file (if recursive) and the entire line. Using `-o` only the matched field will be returned.
- `-h`: Exclude file name for each match
- `-H`: Include file name for each match
- `-l`: files with match. `grep -r -l 'import torch'` lists the files that contain phrase `import torch`.
- `-L`: files without match

### Context

- `-A N`: Include N lines after the match to the output
- `-B N`: Include N lines before the match to the output
- `-C N`: Include N lines before and after the match to the output

---

## `head` and `tail`

Return the first/last few lines.

### flags

- `-c N`: return `N` characters
- `-n N`: return `N` lines
  - `-n +N`: (only for `tail`) return all the lines starting from line `N`.

---

## Remove Columns (`colrm`)

Removes columns from text.

- `colrm M`: Removes character from each lines starting from `M`, i.e., it returns first `M-1` characters of each line.
- `colrm M N`: It removes characters `M` to `N` from each line.

---

## `cut`

Print selected parts of lines. It cuts the line into columns and then subsets from those columns.

### `cut` flags

- `-c`: Selects by character. E.g., Select first 10 characters: `cat file.txt | cut -c1-10`
- `-d`: Uses delimiter for creating fields
- `-f`: Selects by fields. E.g., Select column 1 and 3 from a csv file: `cat file.csv | cut -d, -f1,3`

---

## Generate Sequence (`seq`)

Generate a sequence of numbers. There are three main ways to use this command:

1. `seq NUM`: Generate a sequence from 1 to `NUM` (inclusive).
2. `seq NUM1 NUM2`: Generates a sequence from `NUM1` to `NUM2` (inclusive).
3. `seq NUM1 STEP NUM2`: Generate a sequence starting from `NUM1` to `NUM2` in steps of `STEP`.

__Flags:__

- `-s SEP`: Use `SEP` as separator. Default is new line.
- `-w`: Equal width by padding zeros to left.
- `-f FORMAT`: Format the sequences according to `FORMAT`. `FORMAT` is a printf style formatting string. E.g., `-f '%04g'` to print `4` digits sequences with leading zeros.

---

## Sorting (`sort`)

Sorts lines in a file. Basic usage: `sort file.txt`

### `sort` flags

- `-b`: Ignore leading blanks
- `-h`: Human readable numbers (e.g., 2K, 4M, etc)
- `-M`: Month sort
- `-n`: Numeric sort
- `-r`: Reverse sort
- `-u`: Sort and preserve only unique values
- `--ignore-case`: Case insensitive sort
- `-t`, `--field-separator`: Use a separator
- `-k`, `--key`: Use a key (column) to sort.

Examples:

- Sort by a third column: `sort -t , -k 3`

---

## Split files with `split`

### Split by lines

Split the file based on the number of lines using `-l` flag:

```bash
split -l 10 file
```

Creates multiple files each with 10 lines (except last files).

### Split by number

Split the file into a fix number of files using `-n` flag:

```bash
split -n 5 file
```

Splits the file into 5 files with similar sizes (except last files).

### Split by size

Split the file into file of fixed size using `-b` flag:

```bash
split -b 512 file
```

Splits the file into files of size 512 bytes (except last files). You can also use kilobytes or megabytes, e.g., `split -b 512k file` or `split -b 512m file`.

Another way to achieve this is using `-C` flag, which avoids breaking the lines.

```bash
split -C 512 file
```

__Other Flags:__

- `-d`: Use numeric suffixes, not alphabetic
- `-x`: Use hex suffixes, not alphabetic

---

## `tr`

Translate/Delete characters.

- Replace character: Replace `a` with `A` $\rightarrow$ `tr a A`
- Replace group of characters: Replace `a`, `b`, and `c`, with `A`, `B`, and `C` $\rightarrow$ `tr 'abc' 'ABC'`
- Delete a character: Remove `,` $\rightarrow$ `tr -d ,`
- Translate characters from lower case to upper case: `tr '[:lower:]' '[:upper:]'`

### Interpreted Characters

- `\n`: new line
- `\b`: backspace
- `\r`: return
- `\t`: horizontal tab
- `\v`: Vertical tab
- `[:alnum:]`:all letters and digits
- `[:alpha:]`: all letters
- `[:blank:]`: all whitespace
- `[:digit:]`: all digits
- `[:xdigit:]`: all hexadecimal digits
- `[:lower:]`: all lower case letters
- `[:upper:]`: all upper case letters

---

## `uniq`

Filters adjacent matching lines (`uniq file.txt`). Usually used with sort to get actual unique values (`sort file.txt | uniq`).

### `uniq` flags

- `-u`: Show only unique lines (lines with no repeat).
- `-d`: Show only repeated lines.
- `-c`: Show number of occurrence for each line (line frequency)

Examples:

- Find top 10 most frequent lines: `sort newfile.txt | uniq -c | sort -rn | head -n 10`

---

## Random String Generation

### Using `RANDOM`

environment variable `RANDOM` contains a random integer:

```bash
echo $RANDOM
```

By piping it through md5 checksum, we can get a random string:

```bash
echo $RANDOM | md5sum | head -c 25
```

### Using UUID

Linux kernel has random UUID generator which we can use:

```bash
cat /proc/sys/kernel/random/uuid
```

To get rid of `-` in UUID, we can use `sed` command:

```bash
cat /proc/sys/kernel/random/uuid | sed 's/[-]//g'
```

### Using pseudo random device

In linux `/dev/urandom` generates random numbers. We pass it through `tr` to convert it to string and get the first 20 characters using `head`:

```bash
cat /dev/urandom | tr -dc '[:alpha:]' | head -c 20
```

### Using `base64`

This time we will convert `RANDOM` using `base64`. Note that this only generates 8 characters.

```bash
echo $RANDOM | base64
```

### Using `openssl`

Openssl can generate random outputs in hex and base64 formats:

```bash
openssl rand -hex 20
openssl rand -base64 20
```
