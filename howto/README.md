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

## How to calculate average of a sequence of numbers?

Imagine we have the following file (`nums.txt`) and we want the average of the numbers:

```bash
16.4
81.92
71
16.4
44
28.37
5
4.9
3.63
```

1. Using `awk`: `cat nums.txt | awk '{sum+=$1} END {print sum/NR}'`
2. Using `datamash`: `cat nums.txt | datamash mean 1`
3. Using `bc`: `cat nums.txt | paste -sd+ | bc -l | awk '{print $1/NR}'`
4. Using `jq`: `cat nums.txt | jq -s 'add/length'`
5. Using `csvstat`: `cat nums.txt | csvstat -H --mean`
6. Using `perl`: `cat nums.txt | perl -nle '$sum += $_; $count++; END { print $sum / $count }'`
