
`xargs` is a command-line utility in Unix/Linux that builds and executes command lines from standard input.


It takes input (usually a list of items from a file, pipe, or another command).

It passes those items as arguments to another command.

This is useful when the command you want to run doesn’t accept input from `stdin` directly.

`xargs` = "==take input and turn it into command arguments==."
It’s especially useful in scripts or pipelines when commands don’t read from `stdin`.

----
# Basic

If you have a list of files:
```bash
ls *.txt
```
and you want to remove them, you might try:
```bash
rm < ls *.txt
```
(but `rm` doesn’t read from stdin). Instead, you use `xargs`:
```bash
ls *.txt | xargs rm
```
👉 This runs:
```bash
rm file1.txt file2.txt file3.txt ...
```


# Other examples


Count lines in all `.log` files listed in a file:
```bash
cat filelist.txt | xargs wc -l
```
Download URLs listed in `urls.txt`:
```bash
cat urls.txt | xargs wget
```
Run limited number of parallel processes:
```bash
cat hosts.txt | xargs -n1 -P4 ping -c1
```
`-n1` = one argument per command
`-P4` = run 4 commands in parallel

