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
