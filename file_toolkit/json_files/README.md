# Json Tools

## `jq`

A command-line JSON processor that uses a domain-specific language.

### Installation

```bash
sudo apt install jq
```

### Pretty-print json file

```bash
jq . file.json
```

### Working with arrays

Get all the values from an array or an object (ignoring the keys):

```bash
jq .[] file.json
```

Put the content of a file into an array:

```bash
jq --slurp . file.json
```

Index through an array:

```bash
jq .[5] file.json  # To get 6th element of the array (indices start from zero)
```

### Using Keys

Get all the keys in an object:

```bash
jq keys file.json
```

Get values using key:

```bash
jq .<key_name> file.json
```

Get values from multiple keys:

```bash
jq '.<key1_name>, .<key2_name>' file.json
```

### Functions

- `length`: Returns length of an array
- `select(BOOLEAN)`: Returns the values if the expression is true.

  - Select items where x value is bigger than 10:
        `cat data.json | jq '.points | map(select(.x > 10))'`
- `map(FUNCTION)`: Iterate over an array and get the value of a given key for each element.
    `cat file.json | jq 'map(<function>)'`
- `map_values(OBJECT)`: For iterating over objects.
    `cat file.json | jq 'map_values(<function>)'`

- `add`: Adds elements in an array or object (if they can be added). For numerics, it returns the sum and for strings it returns the concatenation.
    `cat file.json | jq '.values | add'`
- `range`: Returns a sequence of numbers.
  - `range(A)`: Returns numbers from `0` to `A`.
  - `range(A;B)`: Returns numbers from `A` to `B`(exclusive).
  - `range(A;B;C)`: Returns numbers from `A` to `B`(exclusive) increasing by `C`.
- `tonumber`: converts string to number. If the input is number it remains unchanged.
- `tostring`: Prints inputs as string.
- `sort`: Sorts items in an array.
    `cat file.json | jq '.array_key | sort'`
- `sort_by(.KEY)`: Sorts items in an array by the value for the `KEY`.
    `cat file.json | jq '.array_key | sort(.<child_key>)'`
- `reverse`: It reverses an array.
    `cat file.json | jq '.array_key | sort | reverse'`
- `min`, `max`, `unique`: Return minimum, maximum, and unique values in an array.
- `min_by`, `max_by`, `unique_by`: Same as above, but can use a key/path for operation.
- `..`: Allows recursive search for a key.
    `cat file.json | jq '.. | .<key_name>? | select(. != null)'`

### Piping

Apply multiple functions in sequence using `|` operator:

```bash
# Get parent element, then extract value from the key for elements in an array.
cat file.json | jq '.<parent-key> | map(.<child-key>)'
```

```bash
# Get the length of an array.
cat file.json | jq '.<key-name> | length'
```

### Creating new object

```bash
cat file.json | jq '{<new-key1>: .<key1_name>, <new-key2>: .<key2_name>}'
```
