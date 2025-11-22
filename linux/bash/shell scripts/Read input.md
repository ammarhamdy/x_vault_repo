
#### Read command:
+ `read [-options] [variable...]`
+ `variable` is the name of one or more variables used to hold the input value.
+ If no variable name is supplied, the shell variable `REPLY` contains the line of data.
+ Basically, read assigns fields from standard input to the specified variables.
```
#read
#123
#echo $REPLY
#123
```



#### Multivariables:
+ `read` can assign input to multiple variables.
```
#read var1 var2 var3 var4 var5
#echo "var1 = '$var1'"
#echo "var2 = '$var2'"
#echo "var3 = '$var3'"
#echo "var4 = '$var4'"
#echo "var5 = '$var5'"
```


#### Read options:
+ `-a array`:  
	+ Assign the input to `array`, starting with index zero.
+ `-d delimiter`:
	+ The first character in the string delimiter is used to indicate the end of input, rather than a newline character.
+ `-e`:
	+ Use Readline to handle input. 
	+ This permits input editing in the same manner as the command line.
+ `-i string`:
	+ Use `string` as a default reply if the user simply presses ENTER. 
	+ Requires the -e option.
+ `-n num`:
	+ Read num characters of input, rather than an entire line.
+ `-p prompt`:
	+ Display a prompt for input using the string prompt.
+ `-r`:
	+ Raw mode. 
	+ Do not interpret backslash characters as escapes.
+ `-s`:
	+ Silent mode. 
	+ Do not echo characters to the display as they are typed. 
	+ This is useful when inputting passwords and other confidential information.
+ `-t seconds`:
	+ Timeout. 
	+ Terminate input after seconds. 
	+ read returns a non-zero exit status if an input times out.
+ `-u fd`:
	+ Use input from file descriptor fd, rather than standard input.


#### Use secret mode:
```sh
#!/bin/bash
# read-secret: input a secret passphrase

if read -t 10 -sp "Enter secret passphrase > " secret_pass; 
then
	echo -e "\nSecret passphrase = '$secret_pass'"
else
	echo -e "\nInput timed out" >&2
	exit 1
fi
```


#### IFS:
+ Normally, the shell performs word-splitting on the input provided to `read`.
+ This behavior is configured by a shell variable named IFS (for Internal Field Separator).
+ The default value of IFS contains a space, a tab, and a newline character, each of which will separate items from one another.
```
OLD_IFS="$IFS" IFS=":"
read user pw uid gid name home shell <<< "$file_info"
IFS="$OLD_IFS"
```


#### Menu-driven:
+ A common type of interactivity is called menu-driven.
+ In menu-driven programs, the user is presented with a list of choices and is asked to choose one.
