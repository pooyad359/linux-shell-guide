# String Manipulation

## String Length

You could get the length of a string (`var`) using one of the following methods

- `${#var}`
- `expr length $var`

### Length of Matching Substring

Using `expr` we can find the length of a substring that matches a regular expression. There are two methods:
(From the beginning)

1. `expr match $string $pattern`
2. `expr $string : $pattern`

Example:

```bash
string=abcABC123ABCabc
pattern='.*123'
expr $string : $pattern
# Returns: 9
```

## Indexing strings

You could use the following patterns to extract a substring using indices:`{string:position}` or `{string:position:length}`:

```bash
string="abcd-efgh-1234"
echo ${string:5} # Returns: efgh-1234
echo ${string:5:5} # Returns: efgh-
```

Alternatively, you could use `expr substr $string $position $length`

## Regex Extraction

It is similar to getting length of the substring except we need to wrap the expression in `\(` and `\)`:

1. `expr match $string '\($pattern\)`
2. `expr $string : '\($pattern\)'`

---

## Substring Removal

### `${string#pattern}`

Delete shortest match of `pattern` in `$string` from the beginning.

### `${string##pattern}`

Delete longest match of `pattern` in `$string` from the beginning.

### `${string%pattern}`

Delete shortest match of `pattern` in `$string` from the end.

### `${string%%pattern}`

Delete longest match of `pattern` in `$string` from the end.

Example:

```bash
string=abcABC123ABCabc
echo ${string#*ABC} # 123ABCabc
echo ${string##*ABC} # abc
echo ${string%ABC*} # abcABC123
echo ${string%%ABC*} # abc
```

## Substring Replacement

- Replace first match: `${string/substring/replacement}`
- Replace all matches: `${string//substring/replacement}`
- Replace if start matches: `${string/#substring/replacement}`
- Replace if end matches: `${string/%substring/replacement}`

```bash
string=abcABC123ABCabc
echo ${string/abc/XYZ} # XYZABC123ABCabc <- Replaced the first occurrence
echo ${string//abc/XYZ} # XYZABC123ABCXYZ <- Replaced both occurrences
echo ${string/#abc/XYZ} # XYZABC123ABCabc <- Replaced the beginning
echo ${string/#ABC/XYZ} # abcABC123ABCabc <- Didn't match the beginning so didn't replace
echo ${string/%abc/XYZ} # abcABC123ABCXYZ <- Replaced the end
echo ${string/%ABC/XYZ} # abcABC123ABCabc <- Didn't match the end so didn't replace
```
