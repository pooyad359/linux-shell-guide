# Text Operations

## `grep`

Search the content of a file. Simple example is `grep hello hello.txt`, which searches in file `hello.txt` and returns the lines with the word `hello`.

**flags:**

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

## TODO

- [ ] `sed`
- [ ] `sort`
- [ ] `awk`
- [ ] `uniq`
- [ ] `cut`
