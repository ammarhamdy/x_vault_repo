

## `uname`:
+ `uname` command displays information about the current system.
+ To be able to see the name of the kernel you are using, type the following command into the terminal:
```bash
uname
```
+ Execute the `uname` command again twice in the terminal, once with the option `-n` and again with the option `--nodename`. 
+ This will display the network node hostname, also found in the prompt.
```bash
am@ubuntu:~$ uname
Linux
am@ubuntu:~$ uname -n
ubuntu
```


## `pwd`:
+ `pwd` stands for "print working directory". While it doesn't actually "print" in modern versions, older UNIX machines didn't have monitors so the output of commands went to a printer, hence the somewhat misleading name of `pwd`.


## Quotes:
+ To understand single and double quotes, consider that there are times that you don't want the shell to treat some characters as special. 
+ For example, the `*` character is used as a wildcard. 
+ What if you wanted the `*` character to just mean a literal asterisk?
- Single `'` quotes prevent the shell from "interpreting" or expanding all special characters. Often single quotes are used to protect a string (a sequence of characters) from being changed by the shell, so that the string can be interpreted by a command as a parameter to affect the way the command is executed.
- Double `"` quotes stop the expansion of ==glob characters== like the asterisk (`*`), question mark (`?`), and square brackets ( `[]` ). Double quotes do allow for both variable expansion and command substitution (see back quotes) to take place.
- Back `` ` `` quotes cause command substitution which allows for a command to be executed within the line of another command.


## Command inside command:
+ You can also place `$(` before the command and `)` after the command to accomplish command substitution:
```
echo Today is $(date)
```
+ Your output should be similar to the following:
```bash
sysadmin@localhost:~$ echo Today is $(date)
Today is Mon Dec 3 21:33:41 UTC 2018
```                                     
+ Why two different methods that accomplish the same thing? Backquotes look very similar to single quotes, making it harder to "see" what a command is supposed to do.
+ Originally, shells used backquotes; the `$(command)` format was added in a later version of the Bash shell to make the statement more visually clear.
