# Case Command:
+ The multiple-choice compound command is called case.
```bash
case word in
	[pattern [| pattern]...) commands ;;]...
esac
```


## Menu scrpit:
```bash
#!/bin/bash
# case-menu: a menu driven system information program
clear
echo "
Please Select:
1. Display System Information
2. Display Disk Space
3. Display Home Space Utilization
0. Quit"
read -p "Enter selection [0-3] > "
case "$REPLY" in
	0) echo "Program terminated." exit ;;
	1) echo "Hostname: $HOSTNAME" uptime ;;
	2) df -h;;
	3) if [[ "$(id -u)" -eq 0 ]]; then
			echo "Home Space Utilization (All Users)"
			du -sh /home/*
		else
			echo "Home Space Utilization ($USER)"
			du -sh "$HOME"
		fi ;;
	*) echo "Invalid entry" >&2 exit 1 ;;
esac
```


## Patterns:
+ The patterns used by case are the same as those used by pathname expansion (توسع).
Pattern | Description
:-|:-
a)|Matches if word equals a.
\[\[:alpha:\]\])|Matches if word is a single alphabetic character.
???)|Matches if word is exactly three characters long.
\*.txt)|Matches if word ends with the characters .txt.
\*)|Matches any value of word. It is good practice to include this as the last pattern in a case command to catch any values of word that did not match a previous pattern, that is, to catch any possible invalid values.
```bash
#!/bin/bash
read -p "enter word > "
case "$REPLY" in
	[[:alpha:]]) echo "is a single alphabetic character." ;;
	[ABC][0-9]) echo "is A, B, or C followed by a digit." ;;
	???) echo "is three characters long." ;;
	*.txt) echo "is a word ending in '.txt'" ;;
	*) echo "is something else." ;;
esac
```


## multiple patterns:
+ Use or operator.
```bash
case "$REPLY" in
	q|Q) echo "Program terminated." exit ;;
	a|A) echo "Hostname: $HOSTNAME" uptime ;;
	b|B) ...
esac
```


## Performing Multiple Actions:
+ By default after a successful match, the command would terminate.
+ Modern versions of bash add the ;;& notation to terminate each action, so now we can do this:
```bash
#!/bin/bash
# case4-2: test a character
read -n 1 -p "Type a character > "
echo
case "$REPLY" in
	[[:upper:]]) echo "'$REPLY' is upper case." ;;&
	[[:lower:]]) echo "'$REPLY' is lower case." ;;&
	[[:alpha:]]) echo "'$REPLY' is alphabetic." ;;&
	[[:digit:]]) echo "'$REPLY' is a digit." ;;&
	[[:graph:]]) echo "'$REPLY' is a visible char." ;;&
	[[:punct:]]) echo "'$REPLY' is a punctuation symbol." ;;&
	[[:space:]]) echo "'$REPLY' is a whitespace char." ;;&
	[[:xdigit:]]) echo "'$REPLY' is a hexadecimal digit." ;;&
esac
```
+ The addition of the ;;& syntax allows case to continue to the next test rather than simply terminating:
```bash
Type a character > a
'a' is lower case.
'a' is alphabetic.
'a' is a visible character.
'a' is a hexadecimal digit.
```


