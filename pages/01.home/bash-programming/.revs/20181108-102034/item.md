---
title: 'Bash Programming'
taxonomy:
    category:
        - Linux
        - Programming
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

## Special variables

```bash
$# # number of arguments
$@ # array of all arguments
$! # last exit code
```

## Case (switch) statement

```bash
case $1 in
    pattern1 )
        statements
        ;;
    pattern2 )
        statements
        ;;
    ...
esac
```

## Combining Expressions

```bash
[ EXPR1 -a EXPR2 ] # True if both are true
[ EXPR1 -o EXPR2 ] # True if 1 or 2 is true
```

## Add up a list of numbers

```bash
<list of numbers> | paste -sd+ - | bc 
```

## PID

```bash
[ -d $(ps -A | grep 'PATTERN') ] && echo "exists" || echo "not exists"
```

## Programm

```bash
command -v PROGRAMM >/dev/null 2>&1 || { echo >&2 "require foo"; exit 1; }
```

## Search / Replace with sed
```bash
	sed -i \
	        -e "s;^\\(application-port\\)=.*;\\1=8080;g" \
	        -e "s;^\\(application-host\\)=.*;\\1=0.0.0.0;g" \
	        /PATH/TO/FILE
```
search and replace in multiple files
```bash
find . -type f -name 'config' | xargs sed -i -e  's/PATTERN/STRING/g'
```
delete lines containing a pattern from multiple files
```bash
find . -type f -name '*.md' | xargs sed -i -e '/PATTERN/d'
```

## Arrays

```bash
arr=(hello word array)
for i in ${arr[*]}; do
        echo "her is $i"
done
```

## Check if a file is being sourced

Works for bash, ksh. zsh
```bash
([[ -n $ZSH_EVAL_CONTEXT && $ZSH_EVAL_CONTEXT =~ :file$ ]] ||
 [[ -n $KSH_VERSION && $(cd "$(dirname -- "$0")" &&
    printf '%s' "${PWD%/}/")$(basename -- "$0") != "${.sh.file}" ]] ||
 [[ -n $BASH_VERSION && $0 != "$BASH_SOURCE" ]]) || { echo "This script should be sourced for convenience as it sets env variables in your parent shell!"; exit 1; }
```

## Yes no choice selection
```bash
  echo "Continue?"
  select choice in "Yes" "No"; do
    case $choice in
      Yes ) echo "Going on; break;;
      No ) exit;;
    esac
  done
```

## Prevent a script from exiting your shell
If you source a script file any `exit` in a function will exit the shell as it runs in the current shell instead of spawning a subshell. Prevent this behaviour by using `return`!
When a 3rd party script you cannot modify is called which exits your shell than wrap the call with `()` which spawns a subshell for this call

## Printf
More stable and powerful than echo. Comparable to C's function.
```bash
printf "%s with %s\\n" "VAL1" "VAL2" >> test.txt
```

## Empty/clear a file
```bash
echo > FILE
cat /dev/null > FILE
```

## File or directory listings
```bash
find PATH -maxdepth 1 -mindepth 1 -type d -printf '%f\n' | exec -0 ls -l
find PATH -maxdepth 1 -mindepth 1 -type f -not -name README.md | exec -0 ls -l
```

## Check PostgreSQL connection
```bash
apt-get install postgresql-client

while ! pg_isready -h ${HOST} -p ${PORT} &> /dev/null; do
	echo "Connection to ${HOST} ${PORT} failed "
	sleep 1
done
```