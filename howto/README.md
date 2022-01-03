# HOW-TO

## How to get a list of directories?

Option 1:

```bash
ls -d */
```

Option 2:

```bash
ls -l | grep '^d'
```

Option 3:

```bash
find . -maxdepth 1 -type d
```
