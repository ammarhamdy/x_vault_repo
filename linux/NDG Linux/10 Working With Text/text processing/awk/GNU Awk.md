


# AWK


## What is `awk`:
+ A program that you can use to select particular records in a file and perform operations upon them.
+ The _awk_ interpreter may be used for a lot of text-munging and data-processing tasks that require some quick scripting work.
+ The basic function of `awk` is to search files for lines (or other units of text) that contain certain patterns. 
+ When a line matches one of the patterns, `awk` performs specified actions on that line.
+ `awk` continues to process input lines in this way until it reaches the end of the input files.
+ [manual bage](https://www.gnu.org/software/gawk/manual/gawk.html)


## `awk` is a language:
+ `awk` is an _interpreted_ language. 
+ This means that the `awk` utility reads your program and then processes your data according to the instructions in your program.
+ This is different from a _compiled_ language such as C, where your program is first compiled into machine code that is executed directly by your system’s processor.
+ The `awk` utility is thus termed an _interpreter_. 
+ Many modern languages are interpreted.


## To use awk:
+ When you run `awk`, you specify an `awk` _program_ that tells `awk` what to do.
+ The program consists of a series of _rules_.
+ Each rule specifies one pattern to search for and one action to perform upon finding the pattern.
+ Syntactically, a rule consists of a _pattern_ followed by an _action_. The action is enclosed in braces to separate it from the pattern. 
+ Newlines usually separate rules. 
+ Therefore, an `awk` program looks like this:
```sh
pattern { action }
pattern { action }
```


## How to Run `awk` Programs:
+ There are several ways to run an `awk` program. 
+ If the program is short, it is easiest to include it in the command that runs `awk`, like this:
```sh
awk 'program' input-file1 input-file2 …
```
+ When the program is long, it is usually more convenient to put it in a file and run it with a command like this:
```sh
awk -f program-file input-file1 input-file2 …
```
+ Where program consists of a series of patterns and actions


### Running `awk` Without Input Files:
+ `awk` applies the program to the _standard input_, which usually means whatever you type on the keyboard. 
+ This continues until you indicate end-of-file by typing Ctrl-d.
+ As an example, the following program prints a friendly piece of advice:
```sh
>> awk 'BEGIN { print "Don\47t Panic!" }'
Don't Panic!
```
+ `awk` executes statements associated with `BEGIN` before reading any input.
+ If there are no other statements in your program, as is the case here, `awk` just stops, instead of trying to read input.
+ The ‘\47’ is a magic way of getting a single quote into the program, without having to engage in ugly shell quoting tricks.


### `awk` like `cat`:
+ This next simple `awk` program emulates the `cat` utility; it copies whatever you type on the keyboard to its standard output.
```sh
>> awk '{ print }'
Now is the time for all good men
-| Now is the time for all good men
to come to the aid of their country.
-| to come to the aid of their country.
Four score and seven years ago, ...
-| Four score and seven years ago, ...
What, me worry?
-| What, me worry?
Ctrl-d
```


### Running Long Programs:
+ Sometimes `awk` programs are very long. In these cases, it is more convenient to put the program into a separate file. In order to tell `awk` to use that file for its program, you type:
```sh
awk -f source-file input-file1 input-file2 …
```
+ The -f instructs the `awk` utility to get the `awk` program from the file source-file.


### Executable `awk` Programs:
+ Once you have learned `awk`, you may want to write self-contained `awk` scripts, using the ‘#!’ script mechanism.
+ You could update the file advice to look like this:
```sh
#! /bin/awk -f

BEGIN { print "Don't Panic!" }
```
+ After making this file executable (with the `chmod` utility), simply type ‘advice’ at the shell and the system arranges to run `awk` as if you had typed ‘awk -f advice’:
```sh
>> chmod +x advice
>> ./advice
Don't Panic!
```


#### The `#!`:
+ The line beginning with ‘#!’ lists the full file name of an interpreter to run and a single optional initial command-line argument to pass to that interpreter. 
+ The operating system then runs the interpreter with the given argument and the full argument list of the executed program.
+ The first argument in the list is the full file name of the `awk` program. 
+ The rest of the argument list contains either options to `awk`, or data files, or both.
+ Some systems limit the length of the interpreter name to 32 characters. Often, this can be dealt with by using a symbolic link.
+ You should not put more than one argument on the ‘#!’ line after the path to `awk`. It does not work. 
+ The operating system treats the rest of the line as a single argument and passes it to `awk`.


## Shell Quoting Issues:
+ For short to medium-length `awk` programs, it is most convenient to enter the program on the `awk` command line.
+ This is best done by enclosing the entire program in single quotes.


### The null:
+ The null string is character data that has no value.
+ In other words, it is empty. It is written in `awk` programs like this: `""`. 
+ In the shell, it can be written using single or double quotes: `""` or `''`
+ Although the null string has no characters in it.


### The quoting rules:
+ Preceding any single character with a backslash (‘\’) quotes that character.
+ The shell removes the backslash and passes the quoted character on to the command.
+ It is _impossible_ to embed a single quote inside single-quoted text.
+ Double quotes protect most things between the opening and closing quotes. 
+ The shell does at least variable and command substitution on the quoted text.
+ Because certain characters within double-quoted text are processed by the shell, they must be _escaped_ within the text. Of note are the characters:
```
$  `  \  "
```
+ All of which must be preceded by a backslash within double-quoted text if they are to be passed on literally to the program.
```sh
awk 'BEGIN { print "Don\47t Panic!" }'
## OR 
awk "BEGIN { print \"Don't Panic!\" }"
```
+ Note that the single quote is not special within double quotes.
