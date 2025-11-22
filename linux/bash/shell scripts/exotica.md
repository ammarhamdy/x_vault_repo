
# Group Commands and Subshells


## Group commands:
+ bash allows commands to be grouped together. This can be done in one of two ways, either with a group command or with a subshell.
+ Here is the syntax of a group command: 
	+ `{ command1; command2; [command3; ...] }`
+ Here is the syntax of a subshell:
	+ `(command1; command2; [command3;...])`


## Group script:
+ Let’s consider a script segment that performs redirections on multiple commands:
>> `ls -l > output.txt`
>> `echo "Listing of foo.txt" >> output.txt`
>> `cat foo.txt >> output.txt`
+ Using a group command:
>> `{ ls -l; echo "Listing of foo.txt"; cat foo.txt; } > output.txt`
+ Using a subshell is similar:
>> `(ls -l; echo "Listing of foo.txt"; cat foo.txt) > output.txt`
+ When constructing a pipeline of commands, it is often useful to combine the results of several commands into a single stream. Group commands and subshells make this easy.
>> `{ ls -l; echo "Listing of foo.txt"; cat foo.txt; } | lpr`
+ `lpr` to produce a printed report.


## Process Substitution:
+ There is an important difference between group commands and subshells.
+ A group command executes all of its commands in the current shell.
+ A subshell (as the name suggests) executes its commands in a child copy of the current shell.
	+ This means the environment is copied and given to a new instance of the shell. 
	+ When the subshell exits, the copy of the environment is lost, so any changes made to the subshell’s environment (including variable assignment) are lost as well.
+ _Group commands are both faster and require less memory._


## The read and supsheel problem:
>>`echo "foo" | read`
>>`echo $REPLY # it is an empty`
+ The content of the `REPLY` variable is always empty because the read command is executed in a subshell, and its copy of `REPLY` is destroyed when the subshell terminates.


## Process substitution: 
+ The shell provides an exotic form of expansion called process substitution that can be used to work around this problem (The read and supsheel problem).
+ Process substitution is expressed in two ways.
	+ For processes that produce standard output, it looks like this:
		+ `<(list)`
	+ For processes that intake standard input, it looks like this: 
		+ `>(list)`
+ Where list is a list of commands.
+ To solve our problem with read, we can employ process substitution like this:
>> `read < <(echo "foo")`
>> `echo $REPLY`


## Subshell as an ordinary file:
+ Process substitution allows us to treat the output of a subshell as an ordinary file for purposes of redirection.
+ In fact, since it is a form of expansion, we can examine its real value:
>> `echo <(echo "foo")`
> `/proc/self/fd/11`
+ By using echo to view the result of the expansion, we see that the output of the subshell is being provided by a file named `/proc/self/fd/11`


## Process substitution  with a while loop:
+ Process substitution is often used with loops containing read. 
+ Here is an example of a read loop that processes the contents of a directory listing created by a subshell:
```bash
#!/bin/bash
# pro-sub: demo of process substitution

while read attr links owner group size date time filename; 
do
	cat << EOF
		Filename: $filename
		Size: $size
		Owner: $owner
		Group: $group
		Modified: $date $time
		Links: $links
		Attributes: $attr
	EOF
done < <(ls -l | tail -n +2)
```
+ The loop executes read for each line of a directory listing.
+ The listing itself (`ls` command) is produced on the final line of the script.
+ This line redirects the output of the process substitution into the standard input of the loop.



---
# Traps


## Signals:
+ When we design a large, complicated script, it is important to consider what happens if the user logs off or shuts down the computer while the script is running.
+ When such an event occurs, a signal will be sent to all affected processes. In turn, the programs representing those processes can perform actions to ensure a proper and orderly termination of the program.
+ if a signal is received indicating that the program was going to be terminated prematurely, bash provides a mechanism for this purpose known as a **trap**.


## Trap:
+ Traps are implemented with the appropriately named builtin command, trap. 
+ trap uses the following syntax:
	+ `trap argument signal [signal...]`
+ `argument` is a string that will be read and treated as a command and signal is the specification of a signal that will trigger the execution of the interpreted command.
```bash
#!/bin/bash
# trap-demo: simple signal handling demo

trap "echo 'I am ignoring you.'" SIGINT SIGTERM

for i in {1..5}; do
	echo "Iteration $i of 5"
	sleep 5
done
```
+ This script defines a trap that will execute an echo command each time either the `SIGINT` or `SIGTERM` signal is received while the script is running.
+ Execution of the program looks like this when the user attempts to stop the script by pressing `CTRL-C`:
>> trap-demo
> Iteration 1 of 5
> Iteration 2 of 5
> ^CI am ignoring you.
> Iteration 3 of 5
> ^CI am ignoring you.
> Iteration 4 of 5
> Iteration 5 of 5
+ As we can see, each time the user attempts to interrupt the program, the message is printed instead.


## Handel signal: 
+ In this example, a separate shell function is specified for each signal to be handled:
```bash
#!/bin/bash
# trap-demo2: simple signal handling demo

exit_on_signal_SIGINT () {
	echo "Script interrupted." 2>&1
	exit 0
}

exit_on_signal_SIGTERM () {
	echo "Script terminated." 2>&1
	exit 0
}

trap exit_on_signal_SIGINT SIGINT
trap exit_on_signal_SIGTERM SIGTERM

for i in {1..5}; do
	echo "Iteration $i of 5"
	sleep 5
done
```
+ Without an exit, the script would continue after completing the function.


## Temporary files:
+ One reason signal handlers are included in scripts is to remove temporary files that the script may create to hold intermediate results during execution.
+ Traditionally, programs on Unix-like systems create their temporary files in the `/tmp` directory, a shared directory intended for such files.
+ since the directory is shared, this poses certain security concerns, particularly for programs running with superuser privileges. 
+ Aside from the obvious step of setting proper permissions for files exposed to all users of the system, it is important to give temporary files non predictable filenames. 
+ This avoids an exploit known as a **temp race attack**.


## Non predictable:
+ `tempfile=/tmp/$(basename $0).$$.$RANDOM`
+ This will create a filename consisting of the program’s name, followed by its process ID (PID), followed by a random integer.
+ `$$` to obtain the PID.
+ Note, however, that the `$RANDOM` shell variable returns a value only in the range of 1–32767, which is not a large range in computer terms, so a single instance of the variable is not sufficient to overcome a determined attacker.
+ A better way is to use the `mktemp` program.
+ The `mktemp` program accepts a template as an argument that is used to build the filename. The template should include a series of X characters, which are replaced by a corresponding number of random letters and numbers: 
	+ `tempfile=$(mktemp /tmp/foobar.$$.XXXXXXXXXX)`



---
# Asynchronous Execution 


## Parent and child tasks:
+ Launching a script that, in turn, launches one or more child scripts to perform an additional task while the parent script continues to run.
+ That is, what if the parent or child is dependent on the other and one script must wait for the other to finish its task before finishing its own?
+ Bash has a builtin command to help manage asynchronous execution such as this.
+ The `wait` command causes a parent script to pause until a specified process (the child script) finishes.


## Use wait command:
+ To demonstrate this, we will need two scripts. The first is a parent script:
+ First script:
```bash
#!/bin/bash
# async-parent: Asynchronous execution demo (parent)

echo "Parent: starting..."
echo "Parent: launching child script..."

async-child &
# `$!` shell parameter, 
#	will always contain the process ID of 
#	the last job put into the background.
pid=$!

echo "Parent: child (PID= $pid) launched."
echo "Parent: continuing..."

sleep 2

echo "Parent: pausing to wait for child to finish..."

wait "$pid"

echo "Parent: child is finished. Continuin..."
echo "Parent: parent is done. Exiting."
```
+ Second script:
```bash
#!/bin/bash
# async-child: Asynchronous execution demo (child)

echo "Child: child is running..."

sleep 5

echo "Child: child is done. Exiting."
```
+ In the parent script, the child script is launched and put into the background.
+ The process ID of the child script is recorded by assigning the `pid` variable with the value of the `$!` shell parameter, which will always contain the process ID of the last job put into the background.
+ The parent script continues and then executes a wait command with the PID of the child process. This causes the parent script to pause until the child script exits.
>> async-parent
Parent: starting...
Parent: launching child script...
Parent: child (PID= 6741) launched.
Parent: continuing...
Child: child is running...
Parent: pausing to wait for child to finish...
Child: child is done. Exiting.
Parent: child is finished. Continuing...
Parent: parent is done. Exiting.



---
# Named Pipes


## What is the named pipe?
+ In most Unix-like systems, it is possible to create a special type of file called a named pipe.
+ Named pipes are used to create a connection between two processes and can be used just like other types of files.
+ They are not that popular, but they’re good to know about.


## Whose use named pipes:
+ There is a common programming architecture called client-server, which can make use of a communication method such as named pipes.


## client-server:
+ The most widely used type of client-server system is, of course, a web browser communicating with a web server. The web browser acts as the client, making requests to the server, and the server responds to the browser with web pages.


## Just pipes but named:
+ Named pipes behave like files but actually form first-in first-out (FIFO) buffers. 
+ As with ordinary (unnamed) pipes, data goes in one end and emerges out the other.


## Shape of named pipes:
+ With named pipes, it is possible to set up something like this:
	+ `process1 > named_pipe`
+ and this:
	+ `process2 < named_pipe`
+ and it will behave like this:
	+ `process1 | process2`


## Setting Up a Named Pipe:
+ First, we must create a named pipe. 
+ This is done using the `mkfifo `command:
```bash
mkfifo pipe1
ls -l pipe1
# prw-r--r-- 1 me me 0 2018-07-17 06:41 pipe1
```
+ Here we use `mkfifo` to create a named pipe called `pipe1`.
+ Using ls, we examine the file and see that the first letter in the attributes field is `p`, indicating that it is a named pipe.


## Using Named Pipes:
+ To demonstrate how the named pipe works, we will need two terminal windows (or alternately, two virtual consoles). 
+ In the first terminal, we enter a simple command and redirect its output to the named pipe:
>> ls -l > pipe_1
+ After we press ENTER, the command will appear to hang. 
+ This is because there is nothing receiving data from the other end of the pipe yet.
+ When this occurs, it is said that the pipe is blocked.
+ Using the second terminal window, we enter this command:
>> cat < pipe_1
+ ![[Pasted image 20230402175110.png]]

