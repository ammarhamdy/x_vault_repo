#### Exit status:
+ Commands (including the scripts and shell functions we write) issue a value to the system when they terminate called an exit status.
+ This value, which is an integer in the range of 0 to 255, indicates the success or failure of the command’s execution.
+ By convention (مؤتمر), a value of zero indicates success and any other value indicates failure.
+ The shell provides a parameter that we can use to examine the exit status.
```
echo $?
```


#### Stats:
+ `1`-`125` - Command did not complete successfully.
+ `2` - Misuse of shell builtins (according to Bash documentation).
+ `6` - No such device or address.
+ `124` - command times out.
+ `125` - if a command itself failssee: [coreutils](https://www.gnu.org/software/coreutils/manual/html_node/timeout-invocation.html)
+ `126` - if command is found but cannot be invoked (e.g. is not executable).
+ `127` - if a command cannot be found, the child process created to execute it returns that status.
+ `128` - Invalid argument to `exit`.
+ `128`-`254` - fatal error signal "n" - command died due to receiving a signal. The signal code is added to 128 (128 + SIGNAL) to get the status (Linux: `man 7 signal`, BSD: `man signal`).
+ `130` - command terminated due to Ctrl-C being pressed, 130-128=2 (SIGINT).
+ `137` - if command is sent the `KILL(9)` signal (128+9), the exit status of command otherwise.
+ `141` - `SIGPIPE` - write on a pipe with no reader.
+ `143` - command terminated by signal code 15 (128+15=143).
+ `255`* - exit status out of range.


#### Boolean command:
+ The shell provides two extremely simple builtin commands that do nothing except terminate with either a 0 or 1 exit status. The true command always executes successfully, and the false command always executes unsuccessfully.
```
#true
#echo $?
#0
#false
#rcho $?
#1
```


+ [link](https://unix.stackexchange.com/questions/110348/how-do-i-get-the-list-of-exit-codes-and-or-return-codes-and-meaning-for-a-comm)

