

## `Uniq` command:
+ Compared to `sort`, the `uniq` program is lightweight. 
+ `uniq` performs a seemingly trivial task. 
+ When given a sorted ﬁle (or standard input), it removes any duplicate lines and sends the results to standard output. 
+ It is often used in conjunction with `sort` to clean the output of duplicates.
+ While uniq is a traditional Unix tool often used with sort, the GNU version of sort supports a `-u` option, which removes duplicates from the sorted output.
+ `uniq` only removes duplicate lines that are adjacent to each other.


## Uniqe options:
+ `-c`, `--count` 
	+ Output a list of duplicate lines preceded by the number of times the line occurs.
+ `-d`, `--repeated`:
	+ Output only repeated lines, rather than unique lines.
+ `-f`, n `--skip-fields=n`:
	+ Ignore n leading ﬁelds in each line. 
	+ Fields are separated by white-space as they are in `sort`; however, unlike sort, `uniq` has no option for setting an alternate ﬁeld separator.
+ `-i`, `--ignore-case`:
	+ Ignore case during the line comparisons.
+ `-s n`, `--skip-chars=n` :
	+ Skip (ignore) the leading n characters of each line.
+ `-u`, `--unique`:
	+ Output only unique lines. 
	+ Lines with duplicates are ignored.

