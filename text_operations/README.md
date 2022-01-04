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

- `-pBRE`: Returns all the lines but only numbers the lines that match regrular expression `BRE`. E.g., number lines that start with `import`: `nl -b p^def file.txt`
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
- `-w`: Matches the whole words. E.g., `grep -w hi hello.txt` will match the occurance of `hi` and not when it is part of another word like `hide`.
- `-r`: Searches recursively in all files in a directory. Default directory is `./`
- `-c`: Number of occurance per file.
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

## Soritng (`sort`)

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
- `-c`: Show number of occurance for each line

Examples:

- Find top 10 most frequent lines: `sort newfile.txt | uniq -c | sort -rn | head -n 10`

---

## TODO

- [ ] `sed`
- [ ] `awk`
- [ ] `join`
