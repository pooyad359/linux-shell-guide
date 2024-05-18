# Variables

## Basics

### Define a variable

```bash
name="John Doe"
```

### Print the value

```bash
echo "Hello, $name!"
```

### Update the value

```bash
name="Jane Smith"
```

### Using variables in arithmetic operations

```bash
num1=10
num2=5
sum=$((num1 + num2))
echo "The sum of $num1 and $num2 is $sum"
```

### Using variables in command substitution

```bash
current_date=$(date +%Y-%m-%d)
echo "Today's date is $current_date"
```

### Read input into a variable

```bash
echo "What is your name?"
read name
echo "Hello, $name!"
```

### Unset a variable

```bash
name="John Doe"
unset name
echo "Hello, $name!" # This will print "Hello, !"
```

### Length of a variable

You can find the length of a variable using `${#<variable>}`.

```bash
name="John Doe"
echo "length= ${#name}" # This will print "length= 8"
```

## Handling unset variables

### Default Values

```bash
# If name is not set, it will print "Hello, John Doe!"
default_name="John Doe"
echo "Hello, ${name:-$default_name}!"
```

### Error on unset variables

```bash
# If name is not set, it will print an error message
echo "Hello, ${name?"You need to set the name"}!"

# If name is not set or empty, it will print an error message
echo "Hello, ${name:?"You need to set the name"}!"
```

## Substring

### Indexing a string

You can extract a substring from a variable using `${<variable>:<start>}` to get the substring starting from `<start>` to the end of the string.

```bash
name="John Doe"
echo "First name: ${name:0}" # This will print "First name: John Doe"
```

Or you can use `${<variable>:<start>:<length>}` to get the substring starting from `<start>` with a length of `<length>`.

```bash
name="John Doe"
echo "First name: ${name:0:4}" # This will print "First name: John"
```

### Removing a prefix

You can remove a prefix from a variable using `${<variable>#<pattern>}` to remove the shortest match from the beginning of the string.

```bash
name="John Doe"
echo "Hello, ${name#John }!" # This will print "Hello, Doe!"

name="John Francis Doe"
echo "Hello, ${name#* }!" # This will print "Hello, Francis Doe" by removing everything up to the first space
```

To remove the longest match, use `${<variable>##<pattern>}`.

```bash
name="John Francis Doe"
echo "Hello, ${name##* }!" # This will print "Hello, Doe!" by removing everything up to the last space
```

> To get current directory name, you can use `${PWD##*/}`.

### Removing a suffix

You can remove a suffix from a variable using `${<variable>%<pattern>}` to remove the shortest match from the end of the string.

```bash
name="John Francis Doe"
echo "Hello, ${name% *}!" # This will print "Hello, John Francis" by removing everything after the last space
```

To remove the longest match, use `${<variable>%%<pattern>}`.

```bash
name="John Francis Doe"
echo "Hello, ${name%% *}!" # This will print "Hello, John" by removing everything after the first space
```

> To get parent directory name, you can use `${PWD%/*}`.

### Replace a substring

Replace the first occurrence of a substring in a variable using `${<variable>/<substring>/<replacement>}`.

```bash
name="1234abcd4321"
echo "${name/1/one}!" # This will print "one234abcd4321!" by replacing the first occurrence of "1" with "one"
```

To replace all occurrences, use `${<variable>//<substring>/<replacement>}`.

```bash
name="1234abcd4321"
echo "${name//1/one}!" # This will print "one234abcdone23!" by replacing all occurrences of "1" with "one"
```

## Get variables using patterns

You can use patterns to get variables. For example, to get all variables starting with `name`, you can use `${!name*}`.

```bash
name1="John"
name2="Jane"
echo ${!name*} # This will print "name1 name2"
```

> To unset all variables starting with `name`, you can use `unset ${!name*}`.

## Understanding wildcard

Common wildcards:

- `*` - Matches any string, including the empty string. E.g., `*.txt` would match all files ending with `.txt`.
- `?` - Matches any single character. E.g., `?.txt` would match `a.txt`, `b.txt`, etc.
- `[...]` - Matches any one of the enclosed characters. E.g., `[ab].txt` would match `a.txt` and `b.txt`.
- `[!...]` - Matches any character not enclosed. E.g., `[!ab].txt` would match any file except `a.txt` and `b.txt`.
- `{...}` - Matches any of the comma-separated patterns. E.g., `*.{jpg,jpeg}*` would match all files ending with `.jpg` or `.jpeg`.
- `**` - Matches directories recursively. E.g., `**/*.txt` would match all `.txt` files in the current directory and all subdirectories.
- `?()` - Matches zero or one occurrence of the enclosed pattern. E.g., `*.jp?(e)g` would match `jpg` and `jpeg`.
- `*()` - Matches zero or more occurrences of the enclosed pattern. E.g., ` *.jp*(e)g` would match `jpg` and `jpeg`.
- `+()` - Matches one or more occurrences of the enclosed pattern. E.g., ` *.jp+(e)g` would match `jpeg` but not `jpg`.
- `!()` - Matches anything except the enclosed pattern. E.g., `!(*.txt)` would match all files except `.txt` files.
- `@()` - Matches one of the enclosed patterns. E.g., `@(a|b).txt` would match `a.txt` and `b.txt`.
- `[[:class:]]` - Matches any character in the specified class.
  - `[:alnum:]` - Alphanumeric characters.
  - `[:alpha:]` - Alphabetic characters.
  - `[:digit:]` - Digits.
  - `[:lower:]` - Lowercase letters.
  - `[:upper:]` - Uppercase letters.
  - `[:space:]` - Whitespace characters.
  - `[:punct:]` - Punctuation characters.
  - `[:word:]` - Word characters (letters, digits, and underscores).
  - `[:xdigit:]` - Hexadecimal digits.

Some useful examples:

- `ls *.txt` - List all `.txt` files in the current directory.
- `ls [ab].txt` - List `a.txt` and `b.txt`.
- `ls [!ab].txt` - List all `.txt` files except `a.txt` and `b.txt`.
