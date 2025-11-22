# Sort


## Sort command:
+ The sort program sorts the contents of standard input, or one or more ﬁles speciﬁed on the command line, and sends the results to standard output.


## Useful options:
+ `-b`, `--ignore-leading-blanks`:
	+ This option causes sort to ignore leading spaces in lines and calculates sorting based on the ﬁrst non-whitespace character on the line.
+ `-f`, `--ignore-case`:
	+ Make sorting case-insensitive.
+ `-n`, `--numeric-sort`:
	+ Perform sorting based on the numeric evaluation of a string.
	+ Using this option allows sorting to be performed on numeric values rather than alphabetic values.
+ `-r`, `--reverse`: 
	+ Sort in reverse order. 
	+ Results are in descending rather than ascending order.
+ `-k`, `--key=field1[,field2]`:
	+ Sort based on a key ﬁeld located from `field1` to `field2` rather than the entire line.
+ `-m`, `--merge`:
	+ Treat each argument as the name of a presorted (معد مسبقا) ﬁle. 
	+ Merge multiple ﬁles into a single sorted result without performing any additional sorting.
+ `-o`, `--output=file`:
	+ Send sorted output to file rather than standard output.
+ `-t`, `--field-separator=char`:
	+ Deﬁne the ﬁeld-separator character. 
	+ By default ﬁelds are separated by spaces or tabs.


## Sort list by file size:
```shell
>> ls -l /usr/bin/| head
-rwxr-xr-x 1 root root          2206 Apr 10  2022 zless
-rwxr-xr-x 1 root root          1842 Apr 10  2022 zmore
-rwxr-xr-x 1 root root          4577 Apr 10  2022 znew
-rwxr-xr-x 1 root root        865768 Apr 23 23:49 zsh
-rwxr-xr-x 1 root root           852 Feb 25  2022 zsh5
-rwxr-xr-x 1 root root       1276544 Mar 18 22:58 zstd
lrwxrwxrwx 1 root root             4 Mar 18 22:58 zstdcat -> zstd
-rwxr-xr-x 1 root root          3869 Mar 18 22:58 zstdgrep
-rwxr-xr-x 1 root root           197 Mar 18 22:58 zstdless
lrwxrwxrwx 1 root root             4 Mar 18 22:58 zstdmt -> zstd

>> ls -l /usr/bin/ | tail | sort -nrk 5
-rwxr-xr-x 1 root root       1276544 Mar 18 22:58 zstd
-rwxr-xr-x 1 root root        865768 Apr 23 23:49 zsh
-rwxr-xr-x 1 root root          4577 Apr 10  2022 znew
-rwxr-xr-x 1 root root          3869 Mar 18 22:58 zstdgrep
-rwxr-xr-x 1 root root          2206 Apr 10  2022 zless
-rwxr-xr-x 1 root root          1842 Apr 10  2022 zmore
-rwxr-xr-x 1 root root           852 Feb 25  2022 zsh5
-rwxr-xr-x 1 root root           197 Mar 18 22:58 zstdless
lrwxrwxrwx 1 root root             4 Mar 18 22:58 zstdmt -> zstd
lrwxrwxrwx 1 root root             4 Mar 18 22:58 zstdcat -> zstd
```


## Sort based on more than one key:
+ Let’s consider the following ﬁle containing the history of three popular Linux distributions released from 2006 to 2008:
```shell
>> cat distro.txt    
SUSE     10.2            12/07/2006
Fedora   10              11/25/2008
SUSE     11.0            06/19/2008
Ubuntu   8.04            04/24/2008
Fedora   8               11/08/2007
SUSE     10.3            10/04/2007
Ubuntu   6.10            10/26/2006
Fedora   7               05/31/2007
Ubuntu   7.10            10/18/2007
Ubuntu   7.04            04/19/2007
SUSE     10.1            05/11/2006
Fedora   6               10/24/2006
Fedora   9               05/13/2008
Ubuntu   6.06            06/01/2006
Ubuntu   8.10            10/30/2008
Fedora   5               03/20/2006

>> sort distro.txt 
Fedora   10              11/25/2008
Fedora   5               03/20/2006
Fedora   6               10/24/2006
Fedora   7               05/31/2007
Fedora   8               11/08/2007
Fedora   9               05/13/2008
SUSE     10.1            05/11/2006
SUSE     10.2            12/07/2006
SUSE     10.3            10/04/2007
SUSE     11.0            06/19/2008
Ubuntu   6.06            06/01/2006
Ubuntu   6.10            10/26/2006
Ubuntu   7.04            04/19/2007
Ubuntu   7.10            10/18/2007
Ubuntu   8.04            04/24/2008
Ubuntu   8.10            10/30/2008

```
+ we are going to have to sort on multiple keys.
+ We want to perform an alphabetic sort on the ﬁrst ﬁeld and then a numeric sort on the second ﬁeld.
```shell
>> 	sort -k 1,1 -k 2n distro.txt 
Fedora   5               03/20/2006
Fedora   6               10/24/2006
Fedora   7               05/31/2007
Fedora   8               11/08/2007
Fedora   9               05/13/2008
Fedora   10              11/25/2008
SUSE     10.1            05/11/2006
SUSE     10.2            12/07/2006
SUSE     10.3            10/04/2007
SUSE     11.0            06/19/2008
Ubuntu   6.06            06/01/2006
Ubuntu   6.10            10/26/2006
Ubuntu   7.04            04/19/2007
Ubuntu   7.10            10/18/2007
Ubuntu   8.04            04/24/2008
Ubuntu   8.10            10/30/2008
```
+ We speciﬁed a range of ﬁelds to include in the ﬁrst key. 
+ Because we wanted to limit the sort to just the ﬁrst ﬁeld, we speciﬁed `1,1`, which means “start at ﬁeld 1 and end at ﬁeld 1.”
+ we speciﬁed `2n`, which means ﬁeld 2 is the sort key and that the sort should be numeric. 
+ If we do this `sort -k 1,1 -nk 2 distro.txt` that will make the sort numerical to the whole field but we need only second sorted field as  a numerical.
+ An option letter may be included at the end of a key speciﬁer to indicate the type of sort to be performed.


## Sort base on date field:
+ The third ﬁeld in our list contains a date in an inconvenient format for sorting. 
+ On computers, dates are usually formatted in `YYYY-MMDD` order to make chronological sorting easy, but ours are in the American format of `MM/DD/YYYY`. 
+ How can we sort this list in chronological order?
+ The key option allows speciﬁcation of offsets within ﬁelds, so we can deﬁne keys within ﬁelds.
```shell
>> sort -k 3.7nbr -k 3.1nbr -k 3.4nbr distro.txt 
Fedora   10              11/25/2008
Ubuntu   8.10            10/30/2008
SUSE     11.0            06/19/2008
Fedora   9               05/13/2008
Ubuntu   8.04            04/24/2008
Fedora   8               11/08/2007
Ubuntu   7.10            10/18/2007
SUSE     10.3            10/04/2007
Fedora   7               05/31/2007
Ubuntu   7.04            04/19/2007
SUSE     10.2            12/07/2006
Ubuntu   6.10            10/26/2006
Fedora   6               10/24/2006
Ubuntu   6.06            06/01/2006
SUSE     10.1            05/11/2006
Fedora   5               03/20/2006

```
+ By specifying `-k 3.7`, we instruct sort to use a sort key that begins at the seventh character within the third ﬁeld.
+ The `b` option is included to suppress (كبح) the leading spaces (ignore leading (أمامي) blanks) .


## Sort base on specific delimiter:
+ `sort` provides the `-t` option to deﬁne the ﬁeld separator character.
```shell
>> head /etc/passwd | sort -t ":" -k 3
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

```

