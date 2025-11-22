
Transliterate or Delete Characters

----

# Transliterate characters:
+ The tr program is used to transliterate characters. 
+ We can think of this as a sort of character-based search-and-replace operation.
+ Transliteration is the process of changing characters from one alphabet to another.
```shell
>> echo "lowercase letters" | tr a-z A-Z
LOWERCASE LETTERS
```


# Character sets:
+ Character sets may be expressed in one of three ways:
	+ An enumerated list:
		+ For example,`ABCDEFGHIJKLMNOPQRSTUVWXYZ`.
	+ A character range:
		+ For example, `A-Z`.
	+ `POSIX` character classes:
		+ For example, `[:upper:]`.
```shell
>> echo "lowercase letters" | tr [:lower:] A
AAAAAAAAA AAAAAAA
```


# Delete characters:
+ Converting MS-DOS text ﬁles to Unix-style text. 
+ To perform this conversion, carriage return characters need to be removed from the end of each line. 
+ This can be performed with tr as follows:
```shell
>> tr -d '\r' < dos_file > unix_file
```


#  Delete repeated instances:
+ Using the `-s` option, tr can “squeeze” (delete) repeated instances of a character:
```shell
>> echo "aaabbbccc" | tr -s ab
abccc
```
+ Note that the repeating characters must be adjoining.


# ROT13:
+ The not-so-secret decoder ring.
+ The method simply moves each character 13 places up the alphabet. 
+ Because this is halfway up the possible 26 characters, performing the algorithm a second time on the text restores it to its original form.
+ See [wiki ROT13](https://en.wikipedia.org/wiki/ROT13)
```shell
>> echo "secret text" | tr a-zA-Z n-za-mN-ZA-M
frperg grkg

>> echo "frperg grkg" | tr a-zA-Z n-za-mN-ZA-M
secret text

>> echo "abcd-nopq" | tr a-z n-z
nopq-zzzz

>> echo "abcd-nopq" | tr a-z n-za-m
nopq-abcd
```
+ ![[Pasted image 20230520145714.png]]

# Replace null caharacter    
```sh
tr '\000' ' '
```

