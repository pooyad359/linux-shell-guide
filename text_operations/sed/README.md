# Stream Editor (`sed`)

It is used for various text manipulation tasks such as substitution, filtering, removing, etc. The general usage is `sed` command followed by an expression and then a file. The expression is applied to the file and the result is returned.

## Substitution (`s/`)

replaces the part of line matching a regular expression, with the replacement text. `s/` at the beginning specifies a substitution operation. E.g., Replace `abc` at the start of the line with `ABC`: `sed 's/^abc/ABC/g' file.txt`

Another way to use substitution is by specifying a pattern for filtering the lines and then substitution pattern. Try example above but only the lines that have `xyz`: `sed '/xyz/s/^abc/ABC/g' file.txt`. You could reverse the filter by using `!` before `s/`, e.g., `sed '/xyz/!s/^abc/ABC/g' file.txt` for lines that don't start with `xyz`.

`g` at the end of the expression refers to global replacement (i.e., replace all the matches). If not specified, it only replaces the first match. You could also use a value to replace a specific match, e.g., `/3` will only replaces the third match. Adding `g` to the number starts the replacement for that match, e.g., `/3g` will replace third or later matches.

You could also operate on a specific line number, e.g., `3 s/abc/ABC/g` is only applied to the third line. You could also give a range of line numbers separated with comma, e.g., `1,3 s/abc/ABC/g` (You could use `$` as last line number).

## Delete (`d/`)

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

## Filtering

Print lines matching the patter:

```bash
sed -n '/line_pattern/p'
```

Filter by line number:

```bash
sed '5,$p' file.txt # Show lines from 5 to the end
```

## Useful `sed` Examples

- Delete all spaces in front of every line: `sed 's/^[ ^t]*//' file.txt`
- Delete all spaces at the end of every line: `sed 's/[ ^t]*$//' file.txt`
- Delete all spaces in front and at the end of every line: `sed 's/^[ ^t]*//;s/[ ^]*$//' file.txt`

**More examples for `sed` can be found [here](https://linuxconfig.org/learning-linux-commands-sed)**
