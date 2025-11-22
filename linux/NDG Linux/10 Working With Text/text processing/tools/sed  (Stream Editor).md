
+ [manual bag](https://www.gnu.org/software/sed/manual/sed.html)

# Stream editor:
+ The name `sed` is short for stream editor.
+ It performs text editing on a stream of text, either a set of speciﬁed ﬁles or standard input.
+ `sed` is a powerful and somewhat complex program.


# Substitution:
```sh
echo "front" | sed 's/front/back/'
# back
```
+ Commands in `sed` begin with a single letter. 
+ In the previous example, the substitution command is represented by the letter `s` and is followed by the search-and-replace strings, separated by the slash character as a delimiter.


## Substitution command (s command):
+ Most commands in `sed` may be preceded by an address, which speciﬁes which line(s) of the input stream will be edited. 
+ If the address is omitted, then the editing command is carried out on every line in the input stream.
```sh
echo "front" | sed '1s/front/back/'
#back
```
+ If we specify another number, we see that the editing is not carried out since our input stream does not have a line 2.
```sh
echo "front" | sed '2s/front/back/'
#front
```


# Accept any delimiter:
+ The choice of the delimiter character is arbitrary. 
+ By convention, the slash character is often used, but `sed` will accept any character that immediately follows the command as the delimiter. 
+ We could perform the same command this way:
```sh
echo "front" | sed 's_front_back_'
# back
```


# Addresses:
+ Addresses may be expressed in many ways:
	+ `n` :
		+ A line number where n is a positive integer.
	+ `$` :
		+ The last line.
	+ `/regexp/`: 
		+ Lines matching a `POSIX` basic regular expression. 
		+ Note that the regular expression is delimited by slash characters.
		+ Optionally, the regular expression may be delimited by an alternate character.
	+ `addr1,addr2`  :
		+ A range of lines from `addr1` to `addr2`, inclusive. 
		+ Addresses may be any of the single address forms listed earlier.
	+ `first~step` :
		+ Match the line represented by the number first and then each subsequent line at step intervals. 
		+ For example, `1~2` refers to each odd numbered line, and `5~5` refers to the ﬁfth line and every ﬁfth line thereafter.
	+ `addr1,+n` :
		+ Match `addr1` and the following n lines.
	+ `addr!`
		+ Match all lines except `addr`, which may be any of the forms listed earlier.


# Print command (p command):
+ We print a range of lines, starting with line 1 and continuing to line 5. 
+ To do this, we use the `p` command, which simply causes a matched line to be printed. 
+ For this to be effective, however, we must include the option -n (the “no auto-print” option) to cause `sed` not to print every line by default.
```sh
>> text="Albany, N.Y.
Albuquerque, N.M.
Anchorage, Alaska
Asheville, N.C.
Atlanta, Ga.
Atlantic City, N.J.
Austin, Texas
Baltimore, Md.
Baton Rouge, La.
Billings, Mont.
Birmingham, Ala.
Bismarck, N.D.
Boise, Idaho
Boston, Mass.
Bridgeport, Conn."

>> echo $text | sed -n '1,5p'
Albany, N.Y.
Albuquerque, N.M.
Anchorage, Alaska
Asheville, N.C.
Atlanta, Ga.

```


# Regular expression  option:
+ By including the slash-delimited regular expression `/regex/`, we are able to isolate the lines containing it in much the same manner as `grep`.
```sh
>> echo $text | sed -n '/^A/p'
Albany, N.Y.
Albuquerque, N.M.
Anchorage, Alaska
Asheville, N.C.
Atlanta, Ga.
Atlantic City, N.J.
Austin, Texas
```
+ we’ll try negation by adding an exclamation point `(!)` to the address.
```sh
>> echo $text | sed -n '/^A/!p'
Baltimore, Md.
Baton Rouge, La.
Billings, Mont.
Birmingham, Ala.
Bismarck, N.D.
Boise, Idaho
Boston, Mass.
Bridgeport, Conn.

```


# More commands:
+ So far, we’ve looked at two of the `sed` editing commands, `s` and `p` for Substitute and print.
+ Here the `sed` provides a more complete list of the basic editing commands:
	+ `=`:
		+ Output the current line number.
	+ `a`:
		+ Append text after the current line.
	+ `d`:
		+ Delete the current line.
	+ `i`:
		+ Insert text in front of the current line.
	+ `p`:
		+ Print the current line. 
		+ By default, `sed` prints every line and only edits lines that match a speciﬁed address within the ﬁle. 
		+ The default behavior can be overridden by specifying the `-n` option.
	+ `q`:
		+ Exit `sed` without processing any more lines. 
		+ If the `-n` option is not speciﬁed, output the current line.
	+ `Q`:
		+ Exit `sed` without processing any more lines.
	+ `s/regexp/replacement/`:
		+ Substitute the contents of replacement wherever `regexp` is found. 
		+ replacement may include the special character `&`, which is equivalent to the text matched by regexp.
		+ In addition, replacement may include the sequences `\1` through `\9`, which are the contents of the corresponding sub-expressions in `regexp`.
	+ `y/set1/set2`:
		+ Perform transliteration by converting characters from `set1` to the corresponding characters in `set2`.
		+ Note that unlike tr, `sed` requires that both sets be of the same length.


# Use group on regex:
+ `I` option for ignore case (case insensitive).
+ `g` option for replace all matches not only the first. 
```sh
>> text="Thy self thy foe, to thy sweet self too cruel:"
>> echo $text | sed 's_\(thy\)_{\1}_Ig'
{Thy} self {thy} foe, to {thy} sweet self too cruel:
```
+ Remember that `sed` matching a `POSIX` basic regular expression. 


## Use digits on basic regex:
```sh
>> text="1234 1234 1234 5454"
>> echo $text | sed "s_.*\([[:digit:]]\{4\}\)_**** **** **** \1_" 
**** **** **** 5454


>> text="1000 2000 3000 4000"
>> echo $text | sed "s_\([[:digit:]]\{4\}\) \([[:digit:]]\{4\}\) \([[:digit:]]\{4\}\) \([[:digit:]]\{4\}\)_\4 \3 \2 \1_"
4000 3000 2000 1000
```


## Use use extended regex:
+ `-E, -r, --regexp-extended` : use extended regular expressions.
```sh
echo "aaaa 1111 +++" | sed -E "s_(.{4}) (.{4}) (.{4})_\3 \2 \1_"
aaaa 1111 +++
```


# Generating a list of subdomains
```sh
sed 's/$/.example.com/g' subdomains-1000.txt
```


# Online resources
+ [Sed - An Introduction and a tutorial](http://www.grymoire.com/Unix/Sed.html#uh-10a)  
+ [The TLDP Guide](http://tldp.org/LDP/abs/html/x23170.html)  
+ [Some Practical Examples](http://www.folkstalk.com/2012/01/sed-command-in-unix-examples.html)
+ [This particular page on StackOverflow](http://stackoverflow.com/questions/2232200/regular-expression-in-sed-for-masking-credit-card).
+ [Here's](http://www.thegeekstuff.com/2009/10/unix-sed-tutorial-advanced-sed-substitution-examples/) a detailed tutorial covering groups and back-references.


