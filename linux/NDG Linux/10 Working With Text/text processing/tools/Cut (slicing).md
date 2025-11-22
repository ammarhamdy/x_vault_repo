# Slicing and Dicing


## Cut command:
+ Remove Sections from Each Line of Files.
- The cut program is used to extract a section of text from a line and output the extracted section to standard output.
- t can accept multiple ﬁle arguments or input from standard input.
- Options used on `cut` command:
	- `-c target` or `characters=target`:
		- Extract the **portion** (جزء) of the line deﬁned by list.
		- The `target` may consist of one or more comma-separated numerical ranges.
	- `-f target` or `--fields=target`:
		- Extract one or more ﬁelds from the line as deﬁned by `target`
		- The `target` may contain one or more ﬁelds or ﬁeld ranges separated by commas.
	- -`d delim` or `delimiter=delim`:
		- When `-f` is speciﬁed, use `delim` as the ﬁeld delimiting character.
		- By default, ﬁelds must be separated by a single tab character.
	- `--complement`:
		- Extract the entire line of text, except for those portions speciﬁed by `-c `and/or `-f`.


### Extract specific field (column) :
```shell
>> cut -f 2 tabs_in_my.txt
a
1
10
100

```


## Extract field with specific delimiter :
+ When working with ﬁelds, it is possible to specify a different ﬁeld delimiter rather than the tab character. 
+ Here we will extract the ﬁrst ﬁeld from the `/etc/passwd` ﬁle:
```shell
>> head /etc/passwd
root:x:0:0:root:/root:/usr/bin/zsh
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin

>> cut -d ':' -f 1 /etc/passwd 
root
daemon
bin
sys
sync
games
man
lp
mail
news 
```


### Extract  specific characters:
+ Extract first character:
```shell
>> echo "ammar" | cut -c 1
a
```
+ From second to last character:
```shell
>> echo "ammar" | cut -c 2-
mmar
```
+ From third character to fourth character:
```shell
>> echo "ammar" | cut -c 3-4
ma
```


**Tab as a delimiter:**
```sh
cut -f <field_numbers> -d $'\t' <filename>
```