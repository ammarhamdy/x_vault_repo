
# Introduction


## What Are Regular Expressions?
+ Regular expressions are *symbolic notations* used to identify patterns in text.


## Global regular expression print (grep):
+ The name grep is actually derived from the phrase “global regular expression print”.
+ The grep program accepts options and arguments this way, where regex is a regular expression: 
	+ `grep [options] regex [file...]`
```shell
grep -h '^[A-Za-z0-9]' dirlist*.txt
grep -h '^[A-Z]' dirlist*.txt
grep -h '[bg]zip' dirlist*.txt
grep -h '^zip' dirlist*.txt
```



---
# Meta-characters and Literals


## Regular expression meta-characters:
+ `^ $ . [ ] { } - ? * + ( ) | \`
+ All other characters are considered literals (حرفية), though the backslash character is used in a few cases to create meta-sequences, as well as allowing the meta-characters to be escaped and treated as literals instead of being interpreted as meta-characters.


## Language:
+ We can see the language setting of our system using the following command:
	- `echo $LANG`
- The `LANG` variable contains the name of the language and character set used in your **locale**.
- This value was originally determined when you selected an installation language as your Linux version was installed.



### POSIX standards for characters:
+ The Portable Operating System Interface (POSIX).
+ Is a family of standards specified by the IEEE Computer Society for maintaining compatibility between operating systems.
+ The POSIX standards introduced a concept called a **locale**, which could be adjusted to select the character set needed for a particular location.


### Local command:
+ To see the **locale** settings, use the `locale` command:
+ You can opt to have your system use the traditional (ASCII) collation order by changing the value of the LANG environment variable.
```shell
$ local
LANG=en_US.UTF-8
LANGUAGE=en_US:en
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=

```


### Change the local:
+ To change the locale to use the traditional Unix behaviors, set the LANG variable to POSIX.
>> export LANG=POSIX
+ You can make this change permanent by adding this line to your `.bashrc` file: `export LANG=POSIX`



## POSIX character ranges:
+ The POSIX standard includes a number of **character classes** that provide useful ranges of characters.


### POSIX character classes:
+ `[:alnum:]`:
	+ The alphanumeric characters. 
	+ In ASCII, equivalent to: `[A-Za-z0-9]`
+ `[:word:]`:
	+ The same as `[:alnum:]`, with the addition of the underscore (_) character.
+ `[:alpha:]`:
	+ The alphabetic characters.
	+ In ASCII, equivalent to: `[A-Za-z]`
+ `[:blank:]`:
	+ Includes the space and tab characters.
+ `[:cntrl:]`:
	+ The ASCII control codes. 
	+ Includes the ASCII characters `0` through 31 and 127.
+ `[:digit:]`:
	+ The numerals 0 through 9.
+ `[:graph:]`:
	+ The visible characters. 
	+ In ASCII, it includes characters 33 through 126.
	+ See `for i in range(33, 126 + 1): print(chr(i))`
+ `[:lower:]`:
	+ The lowercase letters.
+ `[:punct:]`:
	+ The punctuation characters. 
	+ In ASCII, equivalent to:`[-!"#$%&’()*+,./:;<=>?@[\\\]_`{|}~]`
+ `[:print:]`:
	+ The printable characters. 
	+ All the characters in `[:graph:]` plus the space character.
+ `[:space:]`:
	+ The white-space characters including space, tab, carriage return, newline, vertical tab, and form feed. 
	+ In ASCII, equivalent to: `[ \t\r\n\v\f]`
+ `[:upper:]`:
	+ The uppercase characters.
+ `[:xdigit:]`:
	+ Characters used to express hexadecimal numbers. I
	+ n ASCII, equivalent to: `[0-9A-Fa-f]`


### Use character classes :
+ Could be used like this:
	+ `ls /usr/sbin/[[:upper:]]*`
+ Remember, however, that this is not an example of a regular expression; rather, it is the shell performing path name expansion. 
+ We use it here because POSIX character classes can be used for both.


### Character classes limitation:
+ Even with the character classes, there is still no convenient way to express partial ranges, such as `[A–M]`.



---
# POSIX Basic vs Extended Regular Expressions


## Split regual expression:
+ POSIX also splits regular expression implementations into two kinds: 
	+ basic regular expressions (BRE).  
	+ Extended regular expressions (ERE).
+ The features we have covered so far are supported by any application that is POSIX compliant and implements BRE.


## The difference between BRE and ERE?
+ It’s a matter of meta-characters. 
+ With BRE, the following meta-characters are recognized:
	+ `^ $ . [ ] *`.
+ All other characters are considered literals. 
+ With ERE, the following meta-characters (and their associated functions) are added: 
	+ `( ) { } ? + |`


## Different grep:
+ We need to use a different grep to use ERE.
+ The GNU version of grep also supports extended regular expressions when the -E option is used.



---
# History


## POSIX:
+ During the 1980s, Unix became a very popular commercial operating system, but by 1988, the Unix world was in turmoil (الاضطراب).
+ Many computer manufacturers had licensed the Unix source code from its creators, AT&T, and were supplying various versions of the operating system with their systems. 
+ However, in their efforts to create product differentiation, each manufacturer added proprietary changes and extensions. 
+ _This started to limit the compatibility of the software._ 
+ As always with proprietary vendors, each was trying to play a winning game of “lock in” with their customers. 
+ This dark time in the history of Unix is known today as the `Balkanization`.
+ Enter the Institute of Electrical and Electronics Engineers (IEEE). 
+ In the mid-1980s, the IEEE began developing a set of standards that would define how Unix (and Unix-like) systems would perform.
+ These standards, formally known as IEEE 1003, define the application programming interfaces (APIs), shell, and utilities that are to be found on a standard Unix-like system. 
+ The name POSIX, which stands for Portable Operating System Interface (with the X added to the end for extra snappiness), was suggested by Richard Stallman (yes, that Richard Stallman) and was adopted by the IEEE.



---
# Alternation


## Match more that one:
>> echo "AAA" | grep -E 'AAA|BBB'
>AAA
>>echo "BBB" | grep -E 'AAA|BBB'
>BBB
>echo "CCC" | grep -E 'AAA|BBB'
+ Added the `-E `option to `grep` (though we could have just used the `egrep` program instead).


## List only hidden files:
>> `ls -a | grep -E "^\."` 


## Use grep with h option:
+ ![[Pasted image 20230426120043.png]]



---
# Quantiﬁers


## Match an Element Zero or One Time:
+ This quantiﬁer means, in effect, “make the preceding element optional.”.
+ Lest's say a phone number to be valid if it matched either of these two forms:
	+ `(nnn) nnn-nnnn`.
	+ `nnn nnn-nnnn`.
+ We could construct a regular expression like this:
```shell
^\(?[0-9][0-9][0-9]\)? [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]$
```
+ because the parentheses are normally meta-characters (in ERE), we precede them with backslashes to cause them to be treated as literals instead, Let’s try it:
```shell
$ echo "(555) 123-4567" | grep -E '^\(?[0-9][0-9][0-9]
\)? [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]$'

(555) 123-4567
```


## Match an Element Zero or More Times:
+ Like the `?` meta-character, the `*` is used to denote an optional item; however, unlike the `?`, the item may occur any number of times, not just once.
+ Let’s say we wanted to see whether a string was a sentence; that is:
	+ It starts with an uppercase letter. 
	+ Then contains any number of uppercase.
	+ And lowercase letters and spaces.
	+ And ends with a period.
+ we could use a regular expression like this:
	+ `[[:upper:]][[:upper:][:lower:] ]*\`.
```shell
$ echo "This works." | grep -E ’[[:upper:]][[:upper:][:lower:]
]*\.’

This works.
```


## Match an Element One or More Times:
+ The `+` meta-character works much like the *, except it requires at least one instance of the preceding element to cause a match.
```shell
$ echo "This that" | grep -E '^([[:alpha:]]+ ?)+$'

This that
```


## Match an Element a Speciﬁc Number of Times:
+ The `{` and `}` meta-characters are used to express minimum and maximum numbers of required matches.
+ Simplify our original regular expression from the following:
```
^\(?[0-9][0-9][0-9]\)? [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]$
```
+ to the following:
```
^\(?[0-9]{3}\)? [0-9]{3}-[0-9]{4}$
```


## Random Phone numbers:
```shell
$ for i in {0..10}; do echo ${RANDOM:0:1}; done
1
2
7
3
2
5
1
3
6
3
1

$ for i in {1..10}; do echo "(${RANDOM:0:3}) ${RANDOM:0:3}-${RANDOM:0:4}" >> phone_list.txt; done

$ cat phone_list.txt 
(806) 157-2427
(100) 279-1651
(189) 189-1891
(152) 101-1977
(214) 292-1317
(870) 324-888
(169) 314-2065
(131) 601-2406
(570) 117-2543
(445) 186-1988
```


## Phone numbers validation:
+ One useful method of validation would be to scan the ﬁle for invalid numbers and display the resulting list.
+  `grep` command with `-v`:
	+ `-v, --invert-match`
	+ `select non-matching lines`
```shell
$ grep -Ev '^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$' phone_list.txt
(870) 324-888

```


## Finding Ugly Filenames with ﬁnd:
+ The `find` command supports a test based on a regular expression.
```shell
find . -regex '.*[^-_./0-9a-zA-Z].*'
```


## Searching for Files with locate:
+ The locate program supports both basic (the `--regexp` option) and extended (the `--regex` option) regular expressions.
```shell
locate --regex 'bin/(bz|gz|zip)'
```


## Searching for Text with less and vim:
+ `less` and `vim` both share the same method of searching for text.
+ Pressing the `/` key followed by a regular expression will perform a search.
```shell
less phonelist.txt
(806) 157-2427
(100) 279-1651
(189) 189-1891
(152) 101-1977
(214) 292-1317
(870) 324-888
(169) 314-2065
(131) 601-2406
(570) 117-2543
(445) 186-1988
/^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$
```
+ vim, on the other hand, supports basic regular expressions, so our search expression would look like this:
```shell
/([0-9]\{3\}) [0-9]\{3\}-[0-9]\{4\}
```
+ We can see that the expression is mostly the same; however, many of the characters that are considered meta-characters in extended(ممتد) expressions are considered literals (حرفية) in basic expressions.
+ They are treated only as meta-characters when escaped with a backslash.


## Zgrep:
+ Just like grep but can search on compressed files.
- Look for instances of PATTERN in the input FILEs, using their uncompressed contents if they are compressed.
- Use `zgrep --help` for more.


---
# References


## Online references:
+ [15 Practical Grep Command Examples](http://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)  .
+ [TLDP Examples for Grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html).
+ [text processing](http://tldp.org/LDP/abs/html/textproc.html).


