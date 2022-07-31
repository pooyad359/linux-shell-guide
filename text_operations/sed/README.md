# Stream Editor (`sed`)

It is used for various text manipulation tasks such as substitution, filtering, removing, etc. The general usage is `sed` command followed by an expression and then a file. The expression is applied to the file and the result is returned.

## Substitution (`s/`)

replaces the part of line matching a regular expression, with the replacement text. `s/` at the beginning specifies a substitution operation. E.g.,

- Find `abc` anywhere in a line and replace it with `ABC`: `sed 's/abc/ABC/g' file.txt`
- Replace `abc` at the start of the line with `ABC`: `sed 's/^abc/ABC/g' file.txt`

Another way to use substitution is by specifying a pattern for filtering the lines and then substitution pattern. Try example above but only the lines that have `xyz`: `sed '/xyz/s/^abc/ABC/g' file.txt`. You could reverse the filter by using `!` before `s/`, e.g., `sed '/xyz/!s/^abc/ABC/g' file.txt` for lines that don't start with `xyz`.

`g` at the end of the expression refers to global replacement (i.e., replace all the matches). If not specified, it only replaces the first match. You could also use a value to replace a specific match, e.g., `/3` will only replaces the third match. Adding `g` to the number starts the replacement for that match, e.g., `/3g` will replace third or later matches.

You could also operate on a specific line number, e.g., `3 s/abc/ABC/g` is only applied to the third line. You could also give a range of line numbers separated with comma, e.g., `1,3 s/abc/ABC/g` (You could use `$` as last line number).

**Use `-r` for extended regular expression**

### Print matches

Instead of `/g` use `/p` with `-n` flag, to see the output only when a substitution happened (i.e., when there was a match).

```bash
sed -n 's/test/another test/p' file.txt

```

#### Simple print matches

To simply just print lines that match a specific pattern, use `sed -n /<pattern>/ p`. This will be similar to using `grep`.

### Using delimiters

If you want to replace `/bin/bash` in a file with `/bin/sh`, normally you need to use escape characters. But `sed` provides a better way. Instead of using `/` as delimiter in `sed` you can use something else, which means your command can have `/` in it and it won't be counted as delimiter. Let's use `>` as delimiter:

```bash
sed 's>/bin/bash>/bin/sh>g'
```

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

## Add lines

- Add a line after the match (append): `sed '/PATTERN/ a "SOME TEXT"'`
- Add a line before the match (insert): `sed '/PATTERN/ i "SOME TEXT"'`
- Replace the line with a new line: `sed '/PATTERN/ c "SOME TEXT"'`

## Character Mapping

For mapping a list of characters to a new list of character.
Convert `{}` to `<>`: `sed 'y/{}/<>/'`

## Multiple commands

You can apply multiple `sed` commands at once by separating them with semicolon and using `-e` flag:

```bash
sed -e 's/hello/Hello/; s/world/World/' file.txt
```

## Read Commands from a file

If you are applying multiple commands, using them in command line won't look pretty. You can put the commands in a separate file and invoke them using `-f` (or `--file`) flag followed by name of the file.

```bash
sed -f commands file.txt

```

## Useful `sed` Examples

- Delete all spaces in front of every line: `sed 's/^[ ^t]*//' file.txt`
- Delete all spaces at the end of every line: `sed 's/[ ^t]*$//' file.txt`
- Delete all spaces in front and at the end of every line: `sed 's/^[ ^t]*//;s/[ ^]*$//' file.txt`
- Count the number of lines (similar to `wc -l`): `sed -n '$='`
- Return the line number for lines that match the pattern: `sed -n '/PATTERN/ ='`
- Replace all `'` with `"` (similar to `tr \' \"`): `sed 'y/'"'"'/"/'`

## Other Examples

| Description | Pattern | Input | Output |
|-|-|-|-|
|Use the matched string and put it in `<>`|`sed -r 's/"[a-zA-Z0-9_\.\-]*"/<&>/'`|`{"Hello-There"}`|`{<"Hello-There">}`|
|Use the matched group and put it in `<>`|`sed -r 's/"(\w*)"/<\1>/'`|`"Hello" There`|`<Hello> There`|
|Return matched group|`sed -rn 's/Today is (.*)/\1/p'`|`Today is Monday`|`Monday`|

**More examples for `sed` can be found [here](https://linuxconfig.org/learning-linux-commands-sed)**
