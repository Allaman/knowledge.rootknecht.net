---
title: 'Bash Programming'
taxonomy:
    category:
        - Shell
    author:
        - Knecht
---

## For Loop

## IF Condition

### Env

```bash
if [ "$ENV_VAR" = "true" ] ; then
	echo $ENV_VAR
fi
```
### Files

```bash
[ -a FILE ] # True if file exists
[ -d FILE ] # True if file exists and is a directory
[ -f FILE ] # True if file exists and is a regular file
[ -h FILE ] # True if file exists and is a symbolic link
[ -s FILE ] # True if file exists and its size is greater than 0
[ -rwx FILE ] # True if file exists and is readable, writable, executable
[ FILE1 -nt FILE2 ] # True if FILE1 has been changed more recently or if FILE1 exists and FILE2 does not
[ FILE1 -ot FILE2 ] # True if FILE1 is older or FILE1 exists and FILE2 does not
```
### Strings

```bash
[ -z STRING ] # True if length of STRING is zero
[ STRING1 != STRING2 ] # True if strings are (not) equal
```

## Combining Expressions

```bash
[ EXPR1 -a EXPR2 ] # True if both are true
[ EXPR1 -o EXPR2 ] # True if 1 or 2 is true
```
