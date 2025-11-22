
# If Statements:
+ In normal text:
```shell
X = 5
If X = 5, 
then: Say “X equals 5.”
Otherwise: Say “X is not equal to 5.”
```
+ In bash:
```shell
if commands; 
then 
commands 
[elif commands; then commands...] 
[else commands] 
fi
```
```
x=5
if [ "$x" -eq 5 ]; 
then
echo "x equals 5."
else
echo "x does not equal 5."
fi
```



# Boolean command:
+ The shell provides two extremely simple builtin commands that do nothing except terminate with either a 0 or 1 exit status. The true command always executes successfully, and the false command always executes unsuccessfully.
```shell
#true
#echo $?
#0
#false
#rcho $?
#1
#if false; true; then echo "It's true."; fi
#It's true.
```


# Using test:
+ The command used most frequently with if is test.
+ The test command performs a variety of checks and comparisons.
+ It has two equivalent forms:
	+ `test expression`
	+ `[ expression ]`
+ Where expression is an expression that is evaluated as either true or false.
+ The test command returns an exit status of 0 when the expression is true and a status of 1 when the expression is false.
+ It is interesting to note that both `test` and `[` are actually commands.
+ In bash they are builtins, but they also exist as programs in /usr/bin for use with other shells.


# File Expressions:
| Expression      | Is true if                                                                                                                                    |
| :-------------- | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| file1 -ef file2 | file1 and file2 have the same inode numbers (the two filenames refer to the same file by hard linking).                                       |
| file1 -nt file2 | file1 is newer than file2.                                                                                                                    |
| file1 -ot file2 | file1 is older than file2.                                                                                                                    |
| -b file         | file exists and is a block-special (device) file.                                                                                             |
| -c file         | file exists and is a character-special (device) file.                                                                                         |
| -d file         | file exists and is a directory.                                                                                                               |
| -e file         | file exists.                                                                                                                                  |
| -f file         | file exists and is a regular file.                                                                                                            |
| -g file         | file exists and is set-group-ID.                                                                                                              |
| -G file         | file exists and is owned by the effective group ID.                                                                                           |
| -k file         | file exists and has its “sticky bit” set.                                                                                                     |
| -L file         | file exists and is a symbolic link.                                                                                                           |
| -O file         | file exists and is owned by the effective user ID.                                                                                            |
| -p file         | file exists and is a named pipe (يضخ-قناة).                                                                                                   |
| -r file         | file exists and is readable (has readable permission for the effective user).                                                                 |
| -s file         | file exists and has a length greater than zero.                                                                                               |
| -S file         | file exists and is a network socket.                                                                                                          |
| -t fd           | fd is a file descriptor directed to/from the terminal. This can be used to determine whether standard input/output/error is being redirected. |
| -u file         | file exists and is setuid.                                                                                                                    |
| -w file         | file exists and is writable (has write permission for the effective user).                                                                    |
| -x file         | file exists and is executable (has execute/search permission for the effective user).                                                         |


# Use file expressions:
```shell
#!/bin/bash
# test-file: Evaluate the status of a file 

FILE=~/.bashrc

if [ -e "$FILE" ]; then
	if [ -f "$FILE" ]; then
	echo "$FILE is a regular file."
	fi 
	if [ -d "$FILE" ]; then
	echo "$FILE is a directory."
	fi 
	if [ -r "$FILE" ]; then
	echo "$FILE is readable."
	fi 
	if [ -w "$FILE" ]; then
	echo "$FILE is writable."
	fi 
	if [ -x "$FILE" ]; then
	echo "$FILE is executable/searchable."
	fi
else
	echo "$FILE does not exist"
exit 1
fi 
exit
```



# String Expressions:
| Expressions                             | Is true if                                                                                                                                                  |
| :-------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| string                                  | is not null.                                                                                                                                                |
| -n string                               | The length of string is greater than zero.                                                                                                                  |
| -z string                               | The length of string is zero.                                                                                                                               |
| string1 = string2 or string1 == string2 | string1 and string2 are equal. Single or double equal signs may be used. The use of double equal signs is greatly preferred, but it is not POSIX compliant. |
| string1 != string2                      | string1 and string2 are not equal.                                                                                                                          |
| string1 > string2                       | string1 sorts after string2.                                                                                                                                |
| string1 < string2                       | string1 sorts before string2.                                                                                                                               |



# Use string expressions:
```shell
ANSWER=maybe

if [ -z "$ANSWER" ]; 
	then
	echo "There is no answer." >&2
	exit 1
fi 

if [ "$ANSWER" = "yes" ]; 
	then
	echo "The answer is YES."
elif [ "$ANSWER" = "no" ]; 
	then
	echo "The answer is NO."
elif [ "$ANSWER" = "maybe" ]; 
	then
	echo "The answer is MAYBE."
else
	echo "The answer is UNKNOWN."
fi
```


# Integer Expressions:
| Expression            | Is true if                                     |     |
| :-------------------- | :--------------------------------------------- | --- |
| integer1 -eq integer2 | integer1 is equal to integer2.                 |     |
| integer1 -ne integer2 | integer1 is not equal to integer2.             |     |
| integer1 -le integer2 | integer1 is less than or equal to integer2.    |     |
| integer1 -lt integer2 | integer1 is less than integer2.                |     |
| integer1 -ge integer2 | integer1 is greater than or equal to integer2. |     |
| integer1 -gt integer2 | integer1 is greater than integer2.             |     |


# Use integer expression:
```shell
#!/bin/bash
# test-integer: evaluate the value of an integer. 

INT=-5

if [ -z "$INT" ]; then
	echo "INT is empty." >&2
	exit 1
fi 

if [ "$INT" -eq 0 ]; 
	then
	echo "INT is zero."
else 
	if [ "$INT" -lt 0 ]; 
	then
	echo "INT is negative."
	else
		echo "INT is positive."
	fi 
	if [ $((INT % 2)) -eq 0 ]; 
	then
		echo "INT is even."
	else
		echo "INT is odd."
	fi
fi
```
**String inequality**
```sh
if [ "$str1" != "$str2" ]; then
  echo "Not equal"
fi
```


# A More Modern Version of test:
+ Modern versions of bash include a compound command that acts as an enhanced replacement for test. It uses the following syntax: `[[ expression ]]`.
+ The `[[]]` command is similar to test (it supports all of its expressions) but adds an important new string expression.


# Regex:
+ `string1 =~ regex` This returns true if string1 is matched by the extended regular expression regex.
```shell
INT=-5
if [[ "$INT" =~ ^-?[0-9]+$ ]]; 
	then
	...
```
+ Another added feature of `[[ ]]` is that the == operator supports pattern matching the same way pathname expansion does.
```shell
FILE=foo.bar
if [[ $FILE == foo.* ]]; 
	then
	...
```


# `(( ))`—Designed for Integers:
+ It supports a full set of arithmetic evaluations.
+ Command `(( ))` is part of the shell syntax rather than an ordinary command and it deals only with integers.
+ It is able to recognize variables by name and does not require expansion to be performed.
```shell
#!/bin/bash
# test-integer2a: evaluate the value of an integer. 

INT=-5

if [[ "$INT" =~ ^-?[0-9]+$ ]]; 
then
	if ((INT == 0)); 
	then echo "INT is zero."
	else 
		if ((INT < 0)); 
		then
			echo "INT is negative."
		else
			echo "INT is positive."
		fi 
		if (( ((INT % 2)) == 0)); 
		then[:upper:]
			echo "INT is even."
		else
			echo "INT is odd."
		fi
	fi
else
	echo "INT is not an integer." >&2
	exit 1
fi
```


# Combining Expressions:
+ Expressions are combined by using logical operators.
+ They are AND, OR, and NOT

|Operationtest|`[[ ]]`|`(( ))`|
|:-|:-|:-|
|and|-a|\&\&|
|or|-o|\||
|not|!|\!|
```shell
#!/bin/bash
# test-integer3: determine if an integer is within a 
# specified range of values.

MIN_VAL=1 
MAX_VAL=100
INT=50 
if [[ "$INT" =~ ^-?[0-9]+$ ]]; 
then
if [[ "$INT" -ge "$MIN_VAL" && "$INT" -le "$MAX_VAL" ]]; 
then
...
```



# Control Operators: Another Way to Branch:
+ The && (AND) and || (OR) operators work like the logical operators in the `[[ ]]` compound command.
+ With the && operator, command1 is executed, and command2 is executed if, and only if, command1 is successful.
```shell
command1 && command2
```
+ With the || operator, command1 is executed and command2 is executed if, and only if, command1 is unsuccessful.
```shell
command1 || command2
```
+ Like:
```shell
#mkdir temp && cd temp
```
```
[[ -d temp ]] || mkdir temp
```



