# Command Line Pipes and Redirection:


Normally, when you execute a command, the output is displayed in the terminal window. 
This output (also called a channel) is called standard output, symbolized by the term `stdout`. 
The file descriptor number for this channel is 1.



Standard error (`stderr`) occurs when an error appears during the execution of a command; it has a file descriptor of 2.
To redirect `stderr` use `>>`
```shell
find /etc -name hosts 2> err.txt
```


Standard input, `stdin`, usually is provided by you to a command by typing on the keyboard; it has a file descriptor of 0. 
However, by redirecting standard input, files can also be used as `stdin`.


Use the redirection symbol `>` along with the `echo` command to redirect the output from the normal output of `stdout`.
Note that `1>` is the same as `>`


## Clobbering:
Notice that using one redirection symbol overwrites an existing file. 
This is called "clobbering" a file.
You can avoid clobbering a file by using `>>` instead of `>`




## Find command:
This very flexible command allows searching with a host of options such as filename, size, date, type and permission.
The `find` command will begin the search in the directory specified and recursively search all of the sub-directories.


## Redirect `stdout` and `stderr` into two separate files:
```shell
find /etc -name hosts > std.out 2> std.err
```
To redirect both standard output (`stdout`) and standard error (`stderr`) to one file, first redirect `stdout` to a file and then redirect `stderr` to that same file by using the notation `2>&1`.
```shell
find /etc -name hosts > find.out 2>&1  
```
The `2>&1` part of the command means "send the `stderr` (channel 2) to the same place where `stdout` (channel 1) is going".



## Redirecting `stdin` from a file:
```shell
tr a-z A-Z < myfile
```



## Redirection use `|`:
Another popular form of redirection is to take the output of one command and send it into another command as input.
```shell
cut -d: -f1 /etc/passwd | sort
```



---
# Viewing Large Text Files



## `more` command:
+ While you are in the `more` command, you can view the help screen by pressing the **`h`** key.
+ Searching for a pattern within both the `more` and `less` commands is done by typing the slash **/**, followed by the pattern to find.
+ To move forward to the next match, press the **n** key. With the `less` command you can also move backwards to previous matches by pressing the **N** (capital n) key.



## `head` command:
+ Another way to specify how many lines to output with the `head` command is to use the option `-n -#`, where `#` is the number of lines counted from the bottom of the output to exclude. Notice the minus symbol `-` in front of the `#`. 
+ For example, if the `/etc/passwd` contains 27 lines, the following command will display lines 1-7, excluding the last twenty lines.
```shell
head -n -20 /etc/passwd
```



----
# Searching Text Using Regular Expressions



## `grep` command family:
+ The `grep` command uses basic regular expressions, special characters like wildcards that match patterns in data. The `grep` command returns the entire line containing the pattern that matches.

+ The `-E` option to the `grep` command can be used to perform searches with extended regular expressions, essentially more powerful regular expressions. Another way to use extended regular expressions is to use the `egrep` command.

+ The `fgrep` command is used to match literal characters, ignoring the special meaning of regular expression characters.

```shell
grep -E 'sshd|root|operator' passwd
```
```shell
egrep 'no(b|n)' passwd
```
```shell
head passwd | grep '[0-9]'
```
```shell
grep -E '[0-9]{3}' passwd 
```
