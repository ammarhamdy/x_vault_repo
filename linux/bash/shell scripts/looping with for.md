# For loop


## Form of For loop:
+ It provides a means of processing sequences during a loop.
+ The original for command’s syntax is as follows:
```bash
for variable [in words]; do
	commands
done
```
+ `words` is an optional list of items that will be sequentially assigned to variable.

```bash
for i in A B C D; 
do 
	echo $i; 
done
```

```sh
for i in {0..100}; do echo -e -n "$i\b\b"; sleep 1; done
```

```sh
for i in {0..100}; do printf "\r%03d" "$i"; sleep 1; done
```



## Create a list:
```bash
for i in {A..X}; 
do
	echo $i
done
```


## Use a path name expansion:
```bash
for i in distros*.txt; 
do 
	echo "$i"; 
done
```
+ if the expansion fails to match any ﬁles, the wildcards themselves (`distros*.txt` in the preceding example) will be returned.


## C Language Form:
```bash
for (( expression1; expression2; expression3 )); 
do
	commands
done
```
+ This form is equivalent to the following construct:
```bash
(( expression1 ))
while (( expression2 )); do
	commands
	(( expression3 ))
done
```
+ `expression1` is used to initialize conditions for the loop.
+ `expression2` is used to determine when the loop is ﬁnished.
+ `expression3` is carried out at the end of each iteration of the loop.
```bash
#!/bin/bash
# simple_counter: demo of C style for command
for (( i=0; i<5; i=i+1 )); 
do
	echo $i
done
```


----
# Examples

**Loop over files in a directory**
```bash
for i in *; do if [ -f "$i" ]; then echo $i; fi; done
```

