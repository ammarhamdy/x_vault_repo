
[gnu](https://www.gnu.org/software/coreutils/manual/html_node/paste-invocation.html#paste-invocation)

# Merge Lines of Files


## Paste command:
+ The paste command does the opposite of `cut`. 
+ Rather than extracting a column of text from a ﬁle, it adds one or more columns of text to a ﬁle.
+ It does this by reading multiple ﬁles and combining the ﬁelds found in each ﬁle into a single stream on standard output. 
+ Like `cut`, `paste` accepts multiple ﬁle arguments and/or standard input.


## change fields order:
```shell
>> ls -l /home/am | tr -s ' ' | cut -d ' ' -f -8 > first_8_fields.txt
 
>> ls -l /home/am | tr -s ' ' | cut -d ' ' -f 9 > last_field.txt

>> paste last_field.txt first_8_fields.txt
total 60
bin     drwxr-xr-x 2 am am 4096 Mar 23 07:06
Desktop drwxr-xr-x 2 am am 4096 May 11 22:54
Documents       drwxr-xr-x 5 am am 4096 May 18 16:03
Downloads       drwxr-xr-x 4 am am 4096 May 17 15:19
hackerRank      drwxr-xr-x 3 am am 4096 May 16 15:11
Music   drwxr-xr-x 2 am am 4096 Feb 27 14:48
opt     drwxr-xr-x 2 am am 4096 Apr 13 14:03
Pictures        drwxr-xr-x 3 am am 4096 May 10 19:06
Public  drwxr-xr-x 2 am am 4096 Feb 27 14:48
python  drwxrwxrwx 3 root root 4096 May 16 15:11
temp    drwxr-xr-x 2 am am 4096 May 20 16:34
Templates       drwxr-xr-x 2 am am 4096 Feb 27 14:48
test_venv       drwxr-xr-x 5 root root 4096 May 11 15:14
Videos  drwxr-xr-x 2 am am 4096 Feb 27 14:48
x_vault drwxr-xr-x 7 am am 4096 May 20 16:23
```



```
$ x="aaa\naa\naaa\naa"
$ echo -e $x  | paste -d '+' - - - -
aaa+aa+aaa+aa
```


## Use pate as to join lines
`data.txt` :
```
Snoopy...
why is it that
everything I try turns out wrong?
Sometimes I wonder
if the kids really like me.
```
count the number of `\n` characters.
```
echo -e `cat data.txt` | tr -cd '\n' | wc -c
```
