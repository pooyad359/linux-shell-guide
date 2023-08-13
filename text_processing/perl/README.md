# Perl

`perl` allows you to use Perl language interpreter. This is expecially useful for dealing with regex.

- `-e`: Parse and execute Perl statement
- `-n`: Process line by line (but doesn't print)
- `-p`: Process line by line and print the line after processing it.

When using `-n` you generally need to add print function to display the result. E.g. `perl -n -e 'print if s/.*?(\d+).*/$1/' file.txt`. In this case, only where a match occured the result will be printed. But when using `-p`, if a substitution happen the result after processing is displayed, otherwise the input is printed:  `perl -p -e 's/.*?(\d+).*/$1/' file.txt`

The variable `$_` contains the input line. You can use it to print the output with `-n` or manipulate it inplace so `-p` would print a different value:

```bash
perl -ne 'print "Line: $_"'
perl -pe '$_ = "Line: $_"'
```

- To display the matched line use: `perl -ne 'print if /<pattern>/'`
- To display the group in matched line use: `perl -nle 'print $1 if /<pattern-with-group>/'`
  - Note that there is `\n` after group, as perl will return the results on the same line.
