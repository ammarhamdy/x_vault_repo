# Accessing the Command Line:
+ The shell provides a set of variables called positional parameters that contain the individual words on the command line.
+ The variables are named 0 through 9.
+ Even when no arguments are provided, $0 will always contain the ﬁrst item appearing on the command line, which is the pathname of the program being executed.
```bash
#!/bin/bash
# posit-param: script to view command line parameters
echo "
\$0 = $0
\$1 = $1
\$2 = $2
\$3 = $3
\$4 = $4
\$5 = $5
\$6 = $6
\$7 = $7
\$8 = $8
\$9 = $9
"
```
> ~# posit-param a b c
> $0 = /home/me/bin/posit-param
> $1 = a
> $2 = b
> $3 = c
> $4 =
> $5 =
> $6 =
> $7 =
> $8 =
> $9 =


# Access more than 9:
+ You can actually access more than nine parameters using parameter expansion. 
+ To specify a number greater than nine, surround the number in braces, as in ${10}, ${55}, ${211}, and so on.


## Determining the Number of Arguments:
+ The shell also provides a variable, `$#`, that contains the number of arguments on the command line.


## Shift the arguments:
+ The shift command causes all the parameters to “move down one” each time it is executed. In fact, by using shift, it is possible to get by with only one parameter (in addition to $0, which never changes).
+ Each time shift is executed, the value of `$2` is moved to `$1`, the value of `$3` is moved to` $2`, and so on. The value of $# is also reduced by one.
+ execute a shift to load `$1` with the next argument.
```bash
#!/bin/bash
# posit-param2: script to display all arguments
count=1
while [[ $# -gt 0 ]]; do
	echo "Argument $count = $1"
	count=$((count + 1))
	shift
done
```
>\~# posit-param2 a b c d
>Argument 1 = a
>Argument 2 = b
>Argument 3 = c
>Argument 4 = d


## Base name:
+ The basename command removes the leading portion of a pathname, leaving only the base name of a ﬁle.
```bash
#!/bin/bash
PROGNAME="$(basename "$0")"
echo "$PROGNAME: usage: $PROGNAME file"
```


## The * Special Parameters:
+ If we give this next line as a parameter to \*
> word words with spaces
+ `$*` will split this line by the value of `IFS` like that:
```bash
echo $* # will give each $n a value after the splliting.
$1 = word
$2 = words
$3 = with
$4 = spaces
```
+ `"$*"` will take the whole line as one parameter.
```bash
echo $* # will take the whole as one.
$1 = word words with spaces
```


## The @ Special Parameters:
+ If we give this next line as a parameter to \@
> word words with spaces
+ `$@` will split this line by the value of `IFS` just like `$*`:
```bash
echo $@ # will give each $n a value after the splliting.
$1 = word
$2 = words
$3 = with
$4 = spaces
```
+ `"$@"` will take the first chunk as parameter and the all other chunks as another  parameter.
```bash
echo $* # will take the whole as one.
$1 = word 
$2 = words with spaces
```

