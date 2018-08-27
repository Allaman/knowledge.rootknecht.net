---
title: 'Bash Programming'
taxonomy:
    category:
        - Shell
---

[TOC]

## Shebang

```bash
#!/bin/bash
```

## Debugging

```bash
bash -x script
```

```bash
set -x # start debugging from here
echo Hello World!
set +x # stop debugging from here
```

```bash
set -v # print shell inputs as they are read
echo Hello World!
set +v # stops showing shell inputs
```

```bash
#!/bin/bash -xv # combining options for whole scripts in the shebang
```

## Loops

```bash
for i in $( ls ); do
	echo item: $i
done
```

```bash
for i in `seq 1 10`;
	do
		echo $i
done
```

```bash
COUNTER=0
while [  $COUNTER -lt 10 ]; do
   	echo The counter is $COUNTER
       	let COUNTER=COUNTER+1 
done
```

```bash
COUNTER=20
until [  $COUNTER -lt 10 ]; do
	echo COUNTER $COUNTER
    	let COUNTER-=1
done
```

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
[ -z "STRING" ] # True if length of STRING is zero
[ "STRING1" != "STRING2" ] # True if strings are (not) equal
```

## Integers

```bash
[ NUM1 -eq NUM2 ] # True if NUM1 is equal to NUM2
[ NUM1 -ne NUM2 ] # True if NUM1 is not equal to NUM2
[ NUM1 -gt NUM2 ] # True if NUM1 is greater than NUM2
[ NUM1 -ge NUM2 ] # True if NUM1 is greater or equal to NUM2
[ NUM1 -lt NUM2 ] # True if NUM1 is leass than NUM2
[ NUM1 -le NUM2 ] # True if NUM1 is less than or equal to NUM2
# Former statements work with double parentheses e.g. ((NUM1 <= NUM2))
[ NUM1 -lt NUM2 ]
[ NUM1 -lt NUM2 ]
```

## Combining Expressions

```bash
[ EXPR1 -a EXPR2 ] # True if both are true
[ EXPR1 -o EXPR2 ] # True if 1 or 2 is true
```

## PID

```bash
[ -d $(ps -A | grep 'PATTERN') ] && echo "exists" || echo "not exists"
```