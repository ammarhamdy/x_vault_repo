

# Parameter expansion (توسع):
+ The simplest form of parameter expansion is reﬂected in the ordinary use of variables.
> $a
+ When expanded, this becomes whatever the variable a contains.
+ Simple parameters may also be surrounded by braces.
> ${a}
> a=kali
> echo "$a_file"  # print nothing
> echo "${a}_file"  # kali_file 
+ It can work with numbers also:
> ${11}


## Expansions to Manage Empty Variables:
+ Several parameter expansions are intended to deal with nonexistent and empty variables.
+ These expansions are handy for handling missing positional parameters and assigning default values to parameters. 
+ Here is one such expansion:
> ${parameter:-word}
+ If parameter is unset (i.e., does not exist) or is empty, this expansion results in the value of word.
+ If parameter is not empty, the expansion results in the value of parameter.
> foo=
> echo ${foo:-"substitute value if unset"}
> substitute value if unset
> echo $foo # foo still empty


## Use = in expansion:
+ If parameter is unset or empty, this expansion results in the value of word. 
> ${parameter:=word}
+ If the value of the parameter is empty it will be the value of word instead of being empty.
>foo=
>echo ${foo:="default value if unset"}
>default value if unset
>echo $foo
>default value if unset


## Use ? in expansion:
+ If parameter is unset or empty, this expansion causes the script to exit with an error, and the contents of word are sent to standard error.
> foo=
> echo ${foo:?"parameter is empty"}
> bash: foo: parameter is empty
> echo $?
> 1


## Expansions That Return Variable Names:
+ The shell has the ability to return the names of variables. This is used in some rather exotic (غريب) situations.
+ The `${!prefix*}` and `${!prefix@}`, This expansion returns the names of existing variables with names beginning with prefix.
+ According to the bash documentation, both forms of the expansion perform identically.
+ we list all the variables in the environment with names that begin with BASH:
> echo ${!BASH*}
> BASH BASH_ARGC BASH_ARGV BASH_COMMAND BASH_COMPLETION BASH_COMPLETION_DIR BASH_LINENO BASH_SOURCE BASH_SUBSHELL BASH_VERSINFO BASH_VERSION


---
# String Operations


## Length of string:
+ `${#parameter}`
+ Expands into the length of the string contained by parameter. 
+ Normally, parameter is a string; however, if parameter is either \@ or \*, then the expansion results in the number of positional parameters.
> foo="This string is long."
> echo "${#foo}"
> 20


## Extract a portion of the string:
+ Expansions are used to extract a portion of the string contained in parameter:
	+ `${parameter:offset}`
+ Extract from the offset to the end (zero base index, Inclusive the offset) :
	+ `${parameter:offset:n_characters}`
+ Extract from the offset to the offest plus n_characters.
>foo="This string is long."
>echo ${foo:5}
>string is long.
>echo ${foo:5:6}
>string


## Extract from last index:
+ If the value of offset is negative, it is taken to mean it starts from the end of the string rather than the beginning. Note that negative valuesmust be preceded by a space to prevent confusion with the `${parameter:- word}` expansion.
+ Start from -1 (the last char) going back with the value of offset inclusive the value of offset.
> echo ${foo: -5}
> long.
> echo ${foo: -5:2}
> 10


## Remove portion from the string:
+ The following expansions remove a leading portion of the string contained in parameter deﬁned by pattern.
	+ `${parameter#pattern}` 
	+ `${parameter##pattern}`
+ pattern is a wildcard pattern like those used in pathname expansion.
+ The difference in the two forms is that the `#` form removes the shortest match, while the `##` form removes the longest match.
>foo=file.txt.zip
>echo ${foo#*.}
>txt.zip
>echo ${foo##*.}
>zip



## Remove portion from string from the end:
+ The following are the same as the previous `#` and `##` expansions, except they remove text from the end of the string contained in parameter rather than from the beginning.
	+ `${parameter%pattern}`
	+ `${parameter%%pattern}`
>foo=file.txt.zip
>echo \${foo\%.*}
>file.txt
>echo \${foo\%\%.\*}
>file


## Search and replace:
+ The following expansions perform a search-and-replace operation upon the contents of parameter:
	+ `${parameter/pattern/string}`
	+ `${parameter//pattern/string}`
	+ `${parameter/#pattern/string}`
	+ `${parameter/%pattern/string}`
+ Only the first occurrence of pattern is replaced. 
+ In the `//` form, all occurrences are replaced.
+ In the `/#` form requires that the match occur at the beginning of the string.
+ In the `/%` form requires the match to occur at the end of the string.
+ In every form, `/string` may be omitted, causing the text matched by pattern to be deleted.
```shell
>> line=abCba
>> echo ${line/[[:upper:]]/'.'}

ab.ba
```


## Convert parameter to upper or lower case:
+ Use declar command with `-u` for upper and `-l` for lower:
```shell
#!/bin/bash
# ul-declare: demonstrate case conversion via declare
declare -u upper
declare -l lower
# $1 is positional parameter 1
if [[ $1 ]]; then
	upper="$1"
	lower="$1"
	echo "$upper"
	echo "$lower"
fi
```
> >$ ul-declare aBc
> ABC
> abc


## Use parameter expansions to convert case:
+ In addition to `declare` command, there are four parameter expansions that perform upper/lowercase conversion:
+ `${parameter,,pattern}`:
	+ Expand the value of parameter into all lowercase.
+ `${parameter,pattern}`:
	+ Expand the value of parameter, changing only the first character to lowercase.
+ `${parameter^^pattern}`:
	+ Expand the value of parameter into all uppercase letters.
+ `${parameter^pattern}`:
	+ Expand the value of parameter, changing only the first character to uppercase (capitalization).
+ The pattern is an optional shell pattern that will limit which characters (for example, `[A-F]`) will be converted.



---
# Arithmetic Expansion


## Form of arithmetic expansion:
+ `$((expression))` where expression is a valid arithmetic expression.


## Number Bases:
+ The shell supports integer constants in any base.
+ Notations used to specify the bases:
	+ `number` notation:
		+ By default, numbers without any notation are treated as decimal (base 10) integers.
	+ `0number` notation:
		+ In arithmetic expressions, numbers with a leading zero are considered octal.
	+ `0xnumber` notation:
		+ Hexadecimal notation.
	+ `base#number`:
		+ For number is in base.
>>$ echo $((0xff))
255
>>$ echo $((2#11111111))
255


## Unary Operators:
+ There are two unary operators, `+` and `-`, which are used to indicate whether a number is positive or negative, respectively. An example is `-5`.


## Simple Arithmetic:
+ `+` Addition
+ `-` Subtraction
+ `*` Multiplication
+ `/` Integer division
+ `**` Exponentiation
+ `%` Modulo (remainder)
+ Since the shell’s arithmetic operates only on integers, the results of division are always whole numbers.


## Multiple of 5:
```bash
#!/bin/bash# modulo: demonstrate the modulo operator
for ((i = 0; i <= 20; i = i + 1)); do
	remainder=$((i % 5))
	if (( remainder == 0 )); then
		printf "<%d> " "$i"
	else
		printf "%d " "$i"
	fi
	done
printf "\n"
```
>>$ modulo
<0> 1 2 3 4 <5> 6 7 8 9 <10> 11 12 13 14 <15> 16 17 18 19 <20>


## Assignment:
+ A single = performs assignment. 
+ `foo = 5` says “make foo equal to 5,” .
+ while `==` evaluates equivalence. 
+ `foo == 5` says “does foo equal 5?”.
+ In the shell, this can be a little confusing because the test command accepts a single `=` for string equivalence. 
+ This is yet another reason to use the more modern `[[ ]]` and `(())` compound commands in place of `test`.


## Bit Operations:
+ `~`:
	+ Bitwise negation. 
	+ Negate all the bits in a number.
+ `<<`:
	+ Left bitwise shift. 
	+ Shift all the bits in a number to the left.
+ `>>`:
	+ Right bitwise shift. 
	+ Shift all the bits in a number to the right.
+ `&`:
	+ Bitwise AND.
	+ Perform an AND operation on all the bits in two numbers.
+ `|`:
	+ Bitwise OR. 
	+ Perform an OR operation on all the bits in two numbers.
+ `^`:
	+ Bitwise XOR.
	+ Perform an exclusive OR operation on all the bits in two numbers.


## Expression to boolean :
+ Expressions that evaluate as zero are considered false, while non-zero expressions are considered true. 
+ The `(( ))` compound command maps the results into the shell’s normal exit codes.


## Ternary operator:
+ The strangest of the logical operators is the ternary operator.
+ Performs a stand-alone logical test. 
+ It can be used as a kind of `if/then/else` statement.
+ It acts on three arithmetic expressions (strings won’t work), and if the first expression is true (or non-zero), the second expression is performed. Otherwise, the third expression is performed.
>># a=0
>># ((a<1?++a:--a))
>># echo $a
1
+ Please note that performing assignment within the expressions is not straightforward. 
+ When attempted, bash will declare an error.
>># a=0
>># ((a<1?a+=1:a-=1))
bash: ((: a<1?a+=1:a-=1: attempted ..... (error token is "-=1")
+ This problem can be mitigated by surrounding the assignment expression with parentheses.
>> ((a<1?(a+=1):(a-=1)))


## BC:
+ An Arbitrary (اِعتِباطِيّ) Precision (دقة) Calculator Language.
+ The bc program reads a file written in its own C-like language and executes it. 
+ A bc script may be a separate file, or it may be read from standard input. 
+ The bc language supports quite a few features including variables, loops, and programmer-defined functions.

## Write bc script:
+ We’ll write a bc script to add 2 plus 2:
```bash
/* foo.bc file*/
/* A very simple bc script */
2 + 2
```
>>bc foo.bc
bc 1.06.94
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type warranty.
4
+ bc can also be used interactively:
>># bc –q
2 + 2
4
quit
+ It is also possible to pass a script to bc via standard input:
>># bc < foo.bc
4
+ The ability to take standard input means that we can use here documents, here strings, and pipes to pass scripts. This is a here string example:
>> # bc <<< "2+2"
4
>># bc `<<-` EOF
	scale = 10
	i = $interest / 12
	p = $principal
	n = $months
	a = p * ((i * ((1 + i) ^ n)) / (((1 + i) ^ n) - 1))
	print a, "\n"
EOF







