# Text Operations

## `cat`

Print and concatenate files.
To concatenate multiple files into one: `cat file1 file2 > target`

### `cat` flags

- `-n`: Adds line number to the beginning of each line

---

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

---

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

## `uniq`

Filters adjacent matching lines (`uniq file.txt`). Usually used with sort to get actual unique values (`sort file.txt | uniq`).

### `uniq` flags

- `-u`: Show only unique lines (lines with no repeat).
- `-d`: Show only repeated lines.
- `-c`: Show number of occurrence for each line

Examples:

- Find top 10 most frequent lines: `sort newfile.txt | uniq -c | sort -rn | head -n 10`

---

## Stream Editor (`sed`)

It is used for various text manipulation tasks such as substitution, filtering, removing, etc. The general usage is `sed` command followed by an expression and then a file. The expression is applied to the file and the result is returned.

### Substitution (`s/`)

replaces the part of line matching a regular expression, with the replacement text. `s/` at the beginning specifies a substitution operation. E.g., Replace `abc` at the start of the line with `ABC`: `sed 's/^abc/ABC/g' file.txt`

Another way to use substitution is by specifying a pattern for filtering the lines and then substitution pattern. Try example above but only the lines that have `xyz`: `sed '/xyz/s/^abc/ABC/g' file.txt`. You could reverse the filter by using `!` before `s/`, e.g., `sed '/xyz/!s/^abc/ABC/g' file.txt` for lines that don't start with `xyz`.

`g` at the end of the expression refers to global replacement (i.e., replace all the matches). If not specified, it only replaces the first match. You could also use a value to replace a specific match, e.g., `/3` will only replaces the third match. Adding `g` to the number starts the replacement for that match, e.g., `/3g` will replace third or later matches.

You could also operate on a specific line number, e.g., `3 s/abc/ABC/g` is only applied to the third line. You could also give a range of line numbers separated with comma, e.g., `1,3 s/abc/ABC/g` (You could use `$` as last line number).

### Delete (`d/`)

Deletes a line matching the pattern:

```bash
sed '/line_pattern/d' file.txt
```

Delete a specific line using line number:

```bash
sed '5d' file.txt # Delete line 5
```

Or a range of lines numbers:

```bash
sed '5,$d' file.txt # Delete lines from 5 to the end
```

### Filtering

Print lines matching the patter:

```bash
sed -n '/line_pattern/p'
```

Filter by line number:

```bash
sed '5,$p' file.txt # Show lines from 5 to the end
```

### Useful `sed` Examples

- Delete all spaces in front of every line: `sed 's/^[ ^t]*//' file.txt`
- Delete all spaces at the end of every line: `sed 's/[ ^t]*$//' file.txt`
- Delete all spaces in front and at the end of every line: `sed 's/^[ ^t]*//;s/[ ^]*$//' file.txt`

**More examples for `sed` can be found [here](https://linuxconfig.org/learning-linux-commands-sed)**


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


---

## TODO

- [ ] `awk`
- [ ] `join`
- [ ] `tr` translate/transform text
- [ ] `expand`, `unexpand` change between tabs and spaces
- [ ] `diff`, `comm` for comparing files
- [ ] `fold` breaking lines base on their length
- [ ] `split` split large files into smaller files
- [ ] `join` For each pair of input lines with identical join fields
- [ ] operators: `#`, `%`, etc.
