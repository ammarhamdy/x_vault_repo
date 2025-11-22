

## Man page:
+ Documents that are displayed with the `man` command are called "Man Pages".
+ If the `man` command can find the manual page for the argument provided, then that manual page will be displayed using a command called `less`. 
+ The following table describes useful keys that can be used with the `less` command to control the output of the display:

|Key|Purpose|
|---|---|
|**H** or **h**|Display the help|
|**Q** or **q**|Quit the help or manual page|
|**Spacebar** or **f** or **PageDown**|Move a screen forward|
|**b** or **PageUp**|Move a screen backward|
|**Enter** or **down arrow**|Move down one line|
|**Up arrow**|Move up one line|
|**/** followed by text to search|Start searching forward|
|**?** followed by text to search|Start searching backward|
|**n**|Move to next text that matches search|
|**N**|Move to previous matching text|


## `man -k` and `apropos`:
+ In some cases you may not remember the exact name of the command. 
+ In these cases you can use the `-k` option to the `man` command and provide a keyword argument.
+ For example, execute the following command to display a summary of all man pages that have the keyword "password" in the description
+ Note that the `apropos` command is another way of viewing man page summaries with a keyword.
+  There is no difference between `man -k` and the `apropos` command.


## Different man pages:
+ The different man pages are distinguished by "sections". By default there are nine sections of man pages:
	- Executable programs or shell commands
	- System calls (functions provided by the kernel)
	- Library calls (functions within program libraries)
	- Special files (usually found in `/dev`)
	- File formats and conventions, e.g. `/etc/passwd`
	- Games
	- Miscellaneous (including macro packages and conventions), e.g. `man(7)>`, `groff(7)`
	- System administration commands (usually only for root)
	- Kernel routines
```bash
man -f passwd
```
+ When you type a command such as `man passwd`, the first section is searched and, if a match is found, the man page is displayed.
+ The `man -f passwd` command that you previously executed shows that there is a section 1 man page for passwd: `passwd (1)`. As a result, that is the one that is displayed by default.


## `man -f` and `whatis`:
+ There is no difference between `man -f` and the `whatis` command.
+ Instead of using `man -f` to display all man page sections for a name, you can also use the `whatis` command
```bash
sysadmin@localhost:~$ whatis passwd                   passwd (5)           - the password file              passwd (1)           - change user password           passwd (1ssl)        - compute password hashes 
```


## `where is`:
+ You may just want to find where a command (or its man pages) is located. 
+ This can be accomplished with the `whereis` command:
```bash
sysadmin@localhost:~$ whereis passwd 
passwd: /usr/bin/passwd /etc/passwd /usr/share/man/man5/passwd.5.gz /usr/share/man/man1/passwd.1ssl.gz /usr/share/man/man1/passwd.1.gz                       
```
+ The `whereis` command does not search for just any file, only for commands and man pages.
+ Recall from earlier that there is more than one `passwd` man page on the system. 
+ This is why you see multiple file names and man pages (the files that end in `.gz` are man pages) when you execute the previous command.