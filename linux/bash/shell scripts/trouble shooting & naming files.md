

# Defensive Programming


## A true story.
+ An unfortunate system administrator wrote a script to perform a maintenance task on an important server. 
+ The script contained the following two lines of code:
> cd $dir_name
> rm *
+ If the directory named in the variable, `dir_name`, exists so no problem.
+ But what happens if it does not? 
	+ In that case, the cd command fails, and the script continues to the next line and deletes the ﬁles in the current working directory.
+ it might be wise to ensure that the `dir_name` variable expands into only one word by quoting it and make the execution of `rm` contingent on the success of `cd`.


## Check the directory existance:
> \[\[ -d "\$dir_name" \]\] && cd "\$dir_name" && rm *


## Verifying Input:
+ Only accept numbers from 1 to 3:
> \[\[ \$REPLY =~ ^[0-3]\$ \]\]
+ It will return a zero exit status only if the string entered by the user is a numeral in the range of zero to three.


---
# naming files


## File name:
+ There are only two characters that cannot be included in a ﬁlename. The ﬁrst is the `/` character since it is used to separate elements of a pathname, and the second is the `null` character (a zero byte), which is used internally to mark the ends of strings.


## Gangrous name:
+ If there is a file called `*` what will `rm` do like that?
> rm *
+ Now `rm` command will remove every thing in current directory untill doing that.
> rm ./*
+ always precede wildcards (such as `*` and `?`) with `./ `to prevent misinterpretation by commands. This includes things like *.pdf and ???.mp3, for example.


## Portable filenames:
+ To ensure that a filename is portable between multiple platforms (i.e., different types of computers and operating systems), care must be taken to limit which characters are included in a filename.
+ There is a standard called the POSIX Portable Filename Character Set that can be used to maximize the chances that a filename will work across different systems.
+ The standard is pretty simple. The only characters allowed are the uppercase letters A–Z, the lowercase letters a–z, the numerals 0–9, period (.), hyphen (-), and underscore (_).


---
# Debugging


## Tracing:
+ Bash provides a method of tracing, implemented by the -x option and the set command with the -x option.
```bash
#!/bin/bash -x
# trouble: script to demonstrate common errors
number=1
if [ $number = 1 ]; then
	echo "Number is equal to 1."
else
	echo "Number is not equal to 1."
fi
```
+ When executed, the results look like this:
```bash
[me@linuxbox ~]$ trouble
+ number=1
+ '[' 1 = 1 ']'
+ echo 'Number is equal to 1.'
Number is equal to 1.
```
+ The leading plus signs indicate the display of the trace to distinguish them from lines of regular output.
+ The plus sign is the default character for trace output. It is contained in the PS4 (prompt string 4) shell variable.
+ To add the line number before blus sign:
> export PS4='$LINENO + '


## Trace selected portion:
+ To perform a trace on a selected portion of a script, rather than the entire script, we can use the `set` command with the `-x` option:
```bash
#!/bin/bash
# trouble: script to demonstrate common errors
number=1
set -x # Turn on tracing
if [ $number = 1 ]; then
	echo "Number is equal to 1."
else
	echo "Number is not equal to 1."
fi
set +x # Turn off tracing
```
+ We use the set command with the -x option to activate tracing and the +x option to deactivate tracing. 
+ This technique can be used to examine multiple portions of a troublesome script.





