# What are arrays


## Scalar variables
+ variables that contain a single value.


## Arrays are :
+ Arrays are variables that hold more than one value at a time.
+ Arrays are organized like a table.
+ Arrays in bash are limited to a single dimension.



---
# Creating an Array


## Assignment ans access of array:
+ Example of both the assignment and access of an array element:
>> a\[1\]=foo
>> echo ${a\[1\]}
>foo


## Use declare:
+ An array can also be created with the declare command:
>> declare -a a



---
# Assigning Values to an Array


## Assigning:
+ Values may be assigned in one of two ways. 
+ Single values may be assigned using the following syntax: 
	+ `name[subscript]=value`
	+ where `name` is the name of the array and `subscript` is an integer.
	+ Value is a string or integer assigned to the array element.
+ Multiple values may be assigned using the following syntax:
	+ `name=(value1 value2 ...)`.
	+ Value placeholders are values assigned sequentially to elements of the array.
	+ starting with element zero.
>> days=(Sun Mon Tue Wed Thu Fri Sat)
+ It is also possible to assign values to a specific element by specifying a subscript for each value:
>> days=(\[0\]=Sun \[1\]=Mon \[2\]=Tue \[3\]=Wed \[4\]=Thu \[5\]=Fri \[6\]=Sat)



---
# Accessing Array Elements:


## The hours script:
+ We will construct a script that examines the modification times of the files in a specified directory.
+ Our script will output a table showing at what hour of the day the files were last modified.
```bash
#!/bin/bash
# hours: script to count files by modification time

usage () {
	echo "usage: ${0##*/} directory" >&2
}

# Check that argument is a directory
if [[ ! -d "$1" ]]; 
then
	usage
	exit 1
fi

# Initialize array
for i in {0..23}; 
do 
	hours[i]=0; 
done

# Collect data
# stat command: 
#	Display file or file system status.
# stat -c option: 
#	for use the specified FORMAT instead of the default. 
for i in $(stat -c %y "$1"/* | cut -c 12-13); 
do
	j="${i#0}"
	((++hours[j]))
	((++count))
done

# Display data
echo -e "Hour\tFiles\tHour\tFiles"
echo -e "----\t-----\t----\t-----"

for i in {0..11}; 
do
	j=$((i + 12))
	printf "%02d\t%d\t%02d\t%d\n" \
	"$i" \
	"${hours[i]}" \
	"$j" \
	"${hours[j]}"
done

printf "\nTotal files = %d\n" $count
```



---
# Array Operations


## Outputting the Entire Contents of an Array:
+ The subscripts `*` and `@` can be used to access every element in an array.
+ The `@` notation is the more useful:
```bash
animals=("a dog" "a cat" "a fish")

for i in ${animals[*]}; do echo $i; done
## output:
a
dog
a
cat
a
fish
##


for i in ${animals[@]}; do echo $i; done
## output:
a
dog
a
cat
a
fish
##

for i in "${animals[*]}"; do echo $i; done
## a dog a cat a fish

for i in "${animals[@]}"; do echo $i; done
## output:
a dog
a cat
a fish
##
```


## Determining the Number of Array Elements:
+ Using parameter expansion, we can determine the number of elements:
>> a\[100\]=foo
>> echo ${#a\[@\]} # number of array elements
> 1
+ It is interesting to note that while we assigned our string to element 100, bash reports only one element in the array. 
+ This differs from the behavior of some other languages in which the unused elements of the array (elements 0–99) would be initialized with empty values and counted. 
+ In bash, array elements exist only if they have been assigned a value regardless of their subscript.


##  Finding the Subscripts Used by an Array:
+ As bash allows arrays to contain “gaps” in the assignment of subscripts, it is sometimes useful to determine which elements actually exist.
+ This can be done with a parameter expansion using the following forms:
	+ `${!array[*]}`
	+ `${!array[@]}`
>> foo=(\[2\]=a \[4\]=b \[6\]=c)
>> for i in "${foo\[@\]}"; do echo $i; done
> a
> b
> c
>> for i in "${!foo\[@\]}"; do echo $i; done
> 2
> 4
> 6


## Adding Elements to the End of an Array:
+ By using the `+=` assignment operator, we can automatically append values to the end of an array.
```bash
foo=(a b c)

echo ${foo[@]}
#a b c

foo+=(d e f)

echo ${foo[@]}
#a b c d e f
```


## Sorting an Array:
+ The shell has no direct way of doing this, but it’s not hard to do with a little coding:
```bash
#!/bin/bash
# array-sort: Sort an array

a=(f e d c b a)
echo "Original array: ${a[@]}"

a_sorted=(
	$(
		for i in "${a[@]}"; 
		do 
			echo $i; 
		done 
		| 
		sort
	)
)

echo "Sorted array: ${a_sorted[@]}"
```
+ The script operates by copying the contents of the original array (a) into a second array (a_sorted) with a tricky piece of command substitution.


## Deleting an Array:
+ To delete an array, use the `unset` command:
```bash
foo=(a b c d e f)
echo ${foo[@]}
# output: a b c d e f

unset foo
echo ${foo[@]}
# output:
```
+ `unset` may also be used to delete single array elements:
```bash
foo=(a b c d e f)
echo ${foo[@]}
# output: a b c d e f

unset foo[2]
echo ${foo[@]}
# output: a b d e f

```
+ Interestingly, the assignment of an empty value to an array does not empty its contents.


## Refers to element zero. 
+ Any reference to an array variable without a subscript refers to element zero of the array.


## Associative Arrays:
+ Associative arrays use strings rather than integers as array indexes.
```bash
declare -A colors
colors["red"]="#ff0000"
colors["green"]="#00ff00"
colors["blue"]="#0000ff"

echo ${colors["red"]}
echo ${colors["green"]}
echo ${colors["blue"]}
```
+ Unlike integer indexed arrays, which are created by merely referencing them, associative arrays **must** be created with the `declare` command using the new `-A` option.



---
# Online tutorial
[creek tutorial](https://www.thegeekstuff.com/2010/06/bash-array-tutorial/).


---
# Read array


The `mapfile` command (also known as `readarray`) reads lines from standard input or a file into an array.

**Read from file:**
```sh
readarray my_array < filename.txt
```
Each line becomes an element of the array.

**To print the array:**
```sh
echo "${my_array[@]}"
```
```sh
printf '%s\n' ${arr[@]}
```

**Using `-t` to Remove Trailing Newlines**
```sh
readarray -t my_array < filename.txt
```

**Skip first 2 lines (-s 2):**
```sh
readarray -s 2 -t arr < <(ls -1)
```

**Read only 3 lines (-n 3):**
```sh
readarray -n 3 -t arr < <(ls -1)
```

**Reverse the output**
```sh
printf '%s\n' ${arr[@]} | tac
```

