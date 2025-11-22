
# Non-printing characters


## Cat with "A" option:
+ If we use cat with the -A option, we can see tab-separated ﬁelds.
+ Options:
	+ `-A, --show-all           equivalent to -vET`
	+ `-E, --show-ends          display $ at end of each line`
	+ `-T, --show-tabs          display TAB characters as ^I`
	+ `-v, --show-nonprinting   use ^ and M- notation, except for LFD and TAB`
```shell
>> cat tabs_in_my.txt 
        a       b       c
        1       2       3
        10      20      30
        100     200     300

>> cat -A tabs_in_my.txt    
^Ia^Ib^Ic$
^I1^I2^I3$
^I10^I20^I30$
^I100^I200^I300$
$
$

```
+ Tab character in our text is represented by `^I`. This is a common notation that means `CTRL-I`.


## MS-DOS text vs UNIX text:
+ You may want to use cat to look for non-printing characters in text is to spot hidden carriage returns.
+ Unix ends a line with a linefeed character (ASCII 10), while MS-DOS and its derivatives use the sequence carriage return (ASCII 13) and linefeed to terminate each line of text.


## Convert from DOS to UNIX format:
+ There are several ways to convert ﬁles from DOS to Unix format.
+ On many Linux systems, there are programs called `dos2unix` and `unix2dos`, which can convert text ﬁles to and from DOS format.


## Cat with n and s option:
+ `-n` or `--number` option numbers lines.
+ `-s` or `--squeeze-blank` option suppresses (يقمع) the output of multiple blank lines.


