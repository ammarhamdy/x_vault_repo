

#### Variables and Constants:
+ When the shell encounters (لقاءات) a variable, it automatically creates it.
+ This differs from many programming languages in which variables must be explicitly declared or defined before use.
+ The shell is very lax about this, which can lead to some problems:
```
#foo="yes"
#echo $foo
yes
#echo $fool
#
```
+ We display the value of the variable name misspelled as fool and get a blank result.
+ This is because the shell happily created the variable fool when it encountered it and gave it the default value of nothing, or empty.


#### Use braces {}:
+ It’s good practice is to enclose variables and command substitutions in double quotes to limit the effects of word-splitting by the shell.
+ Quoting is especially important when a variable might contain a filename.
```
#foo="yes"
#echo $foo
yes
#echo ${foo}l
#yes1
```


#### Rules about variable names:
+ Variable names may consist of alphanumeric character (letters and numbers) and underscore characters.
+ The first character of a variable name must be either a letter or an underscore.
+ Spaces and punctuation symbols are not allowed.


#### use upper case for const:
+ The variable with upper case letter not actually being const but it is a good practice
```
CURRENT_TIME="$(date +"%x %r %Z")"
```


#### Constant:
+ The shell actually does provide a way to enforce the immutability of constants, through the use of the declare built-in command with the -r (read-only) option.
```
declare -r TITLE="Page Title"
```



#### Data type:
+ the shell does not care about the type of data assigned to a variable; it treats them all as strings.
+ You can force the shell to restrict the assignment to integers by using the declare command with the -i option.


#### Assignment:
+ Note that in an assignment, there must be no spaces between the variable name, the equal sign, and the value. So, what can the value consist of? It can have anything that we can expand into a string.
+ Multiple variable assignments may be done on a single line.
```
a=5 b="a string"
```


#### Here Documents:
+ There is a way called a here document or here script of outputting our text.
+ A here document is an additional form of I/O redirection in which we embed a body of text into our script and feed it into the standard input of a command.
```
command << token
text
token
```
```
cat << _EOF_ 
<html> 
	<head> 
		<title>$TITLE</title> 
	</head> 
	<body> 
		<h1>$TITLE</h1> 
		<p>$TIMESTAMP</p>
		<p>is't is't</p>
		<p>"qouets"</p>
	</body> 
</html>
_EOF_
```

+ The shell pays no attention to the quotation marks. It treats them as ordinary characters.
+ If we change the redirection operator from << to <<-, the shell will ignore leading tab characters (but not spaces) in the here document.

