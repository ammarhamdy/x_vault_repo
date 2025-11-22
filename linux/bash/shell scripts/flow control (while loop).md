

# While


## Structure of while:
+ The syntax of the while command is as follows:
```sh
while commands; do commands; done
```


## From 1 to 5:
```sh
#!/bin/bash
# while-count: display a series of numbers 

count=1

while [[ "$count" -le 5 ]]; 
do
	echo "$count"
	count=$((count + 1)) 
done

echo "Finished."
```



---
# Breaking Out of a Loop


## Break and continue:
+ bash provides two builtin commands that can be used to control program flow inside loops.
+ The `break` command immediately terminates a loop.
+ The continue command causes the remainder of the loop to be skipped, and program control resumes with the next iteration of the loop.



---
# until


## Until:
+ The until compound command is much like while, except instead of exiting a loop when a non-zero exit status is encountered, it does the opposite. 
+ An until loop continues until it receives a zero exit status.
```sh
#!/bin/bash
# until-count: display a series of numbers 

count=1

until [[ "$count" -gt 5 ]]; 
do
	echo "$count"
	count=$((count + 1)) 
done

echo "Finished."
```



---
# Reading Files with Loops


## Process stantder input:
+ `while` and `until` can process standard input.
```sh
#!/bin/bash
# while-read: read lines from a file

while read distro version release; 
do
	printf "Distro: %s\tVersion: %s\tReleased: %s\n" \
		"$distro" \ 
		"$version" \ 
		"$release"
done < distros.txt
```
+ The loop will use read to input the fields from the redirected file.
+ The read command will exit after each line is read, with a zero exit status until the end-of-file is reached.
+ It is also possible to pipe standard input into a loop:
```sh
#!/bin/bash
# while-read2: read lines from a file

sort -k 1,1 -k 2n distros.txt | while read distro version release; 
do
	printf "Distro: %s\tVersion: %s\tReleased: %s\n" \
		"$distro" \ 
		"$version" \ 
		"$release"
done
```



---


**loop for lines from file**
```bash
while IFS= read -r line; do
    echo "$line"
done < filename.txt
```
Explanation:
`IFS=` prevents leading/trailing white-space from being trimmed.
`-r` prevents backslashes from being interpreted as escape characters.
`< filename.txt` reads the file line-by-line into the loop.


---
# Redirect file content to while loop

```sh
DOMAIN="${1}"
FILE="${2}"

# Read the file from standard input and echo the full domain
while read -r subdomain; do
    echo "${subdomain}.${DOMAIN}"
done < "${FILE}"
```
Rnu:
```sh
./script.sh example.com subs.txt
```
Explain:
```sh
while read -r subdomain; do ... done < "${FILE}"
```
- This loops over each line of the file `subs.txt`.
- ==Each line== gets stored in the variable `subdomain`.
```sh
done < "${FILE}"
```
- **It means:** _feed the contents of `${FILE}` into the `while read` loop._
- Without it, `read` would just wait for user input from the keyboard (standard input).
- With it, the script reads line by line from the file you specified as argument `$2`.

