

# Shell Scripts in a Nutshell


A shell script is a file of executable commands that has been stored in a text file. 
When the file is run, each command is executed. 
Shell scripts have access to all the commands of the shell, including logic.

The script is run as an argument to the shell:
```shell
sh test.sh
```

The script is run directly from the shell:
```shell
./test.sh
```

```shell
#!/bin/sh
echo "Hello, World!"
```
The two characters `#!` are traditionally called the hash and the bang respectively, which leads to the shortened form of  “shebang” when they’re used at the beginning of a script.

 Any text file marked as executable will be run under the interpreter specified in the first line as long as the script is run directly.
 
  If the script is invoked directly as an argument to an interpreter, such as `sh script` or `bash script`, the given shell will be used no matter what’s in the shebang line.


---
# Editing Shell Scripts


Helpful commands for `nano` editor you might need are:

| Command                                    | Description                                               |
| ------------------------------------------ | --------------------------------------------------------- |
| **Ctrl** + **W**                           | search the document                                       |
| **Ctrl** + **W**, then **Control** + **R** | search and replace                                        |
| **Ctrl** + **G**                           | show all the commands possible                            |
| **Ctrl** + **Y**/**V**                     | page up / down                                            |
| **Ctrl** + **C**                           | show the current position in the file and the file’s size |


---
# Scripting Basics


There are 3 topics you must become familiar with:
1. Variables, which hold temporary information in the script.
2. Conditionals, which let you do different things based on tests you write.
3. Loops, which let you do the same thing over and over.



## Variables


There are some special variables in addition to the ones you set.
You can pass arguments to your script:
```shell
#!/bin/bash
echo "Hello $1"
```
A dollar `$` sign followed by a number N corresponds to the Nth argument passed to the script. 
If you call the example above with `./test.sh World` the output will be `Hello World`. 
The `$0` variable contains the name of the script itself.


### Exit code: 
After a program runs, be it a binary or a script, it returns an exit code which is an integer between 0 and 255.
You can test this through the `$?` variable to see if the command completed successfully.

An exit code of `0` means “everything is OK”




## Conditionals


```shell
if somecommand; then
  # do this if somecommand has an exit code of 0
fi
```


## Test command:
The `test` command gives you easy access to comparison and file test operators.
For example:

| Command\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | Description                                                         |
| ----------------------------------------- | ------------------------------------------------------------------- |
| `test –f /dev/ttyS0`                      | `0` if the file exists                                              |
| `test ! –f /dev/ttyS0`                    | `0` if the file doesn’t exist                                       |
| `test –d /tmp`                            | `0` if the directory exists                                         |
| `` test –x `which ls` ``                  | substitute the location of `ls` then `test` if the user can execute |
| `test 1 –eq 1`                            | `0` if numeric comparison succeeds                                  |
| `test ! 1 –eq 1`                          | `NOT – 0` if the comparison fails                                   |
| `test 1 –ne 1`                            | Easier, `test` for numeric inequality                               |
| `test “a” = “a”`                          | `0` if the string comparison succeeds                               |
| `test “a” != “a”`                         | `0` if the strings are different                                    |
| `test 1 –eq 1 –o 2 –eq 2`                 | `-o` is OR: either can be the same                                  |
| `test 1 –eq 1 –a 2 –eq 2`                 | `-a` is AND: both must be the same                                  |
There are many more tests, such as `–gt` for greater than, ways to test if one file is newer than the other
Consult the `test` `man` page for more.

```
am@ubuntu:~$ test -f /dev/ammar
am@ubuntu:~$ echo $?
1
```


### Alias for test command:
There is an alias for it called `[` (left square bracket). 
If you enclose your conditions in square brackets, it’s the same as running `test`.

```shell
if test –f /tmp/foo; then
if [ -f /tmp/foo]; then
```


```shell
#!/bin/bash

if [ "$1" = "hello" ]; then
  echo "---"
elif [ "$1" = "goodbye" ]; then
  echo "---"
else
  echo "---"
fi
```
Note that the `$1` variable is quoted and the string comparison operator is used instead of the numeric version (`-eq`).



## The `case` statement:
```shell
#!/bin/bash

case "$1" in
hello|hi)
  echo "---"
  ;;
goodbye)
  echo "---"
  ;;
*)
  echo "---"
esac
```


## Loops

`for` loops are used when you have a finite collection over which you want to iterate, such as a list of files.

```sh
#!/bin/bash

SERVERS="servera serverb serverc"
for S in $SERVERS; do
  echo "... $S"
done
```
```output
servera
serverb
serverc
```

```sh
#!/bin/bash

for NAME in Sean Jon Isaac David; do
  echo "Hello $NAME"
done

for S in *; do
  echo "Doing something to $S"
done
```
The second loop uses a `*` which is a file glob. 
This gets expanded by the shell to all the files in the current directory.


The other type of loop, a `while` loop, operates on a list of unknown size.
```sh
#!/bin/bash

i=0
while [ $i -lt 10 ]; do
  echo $i
  i=$(( $i + 1))
done
echo “Done counting”
```




```sh
for name in /etc/passwd /etc/hosts /etc/group
do
          wc $name
done
```


```sh
ls
for num in `seq 1 12`
do
          touch test$num
done
ls
```
```sh
am@ubuntu:~/tempo$ for i in `seq 1 12`; do echo ">>$i"; done
>>1
>>2
>>3
>>4
>>5
>>6
>>7
>>8
>>9
>>10
>>11
>>12
```