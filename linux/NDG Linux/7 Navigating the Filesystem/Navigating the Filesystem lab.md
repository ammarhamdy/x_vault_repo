

## Directories realy is a file:
+ Directories are actually files, too; the data that they hold are the names of the files that have been entered into them, along with the inode number (a unique identifier number assigned to each file) for where the data for that file exists on the disk.


## Tilde `~` character:
+ Use the `echo` command below to display some other examples of using the tilde as part of the path:
```bash
am@ubuntu:~$ echo ~
/home/am
```



## Colorful `ls` command:
+ The color indicates what type the item is. 
+ The following table describes some of the more common colors:

| Color | Type of File |
| ---- | ---- |
| Black or White | Regular file |
| Blue | Directory file |
| Cyan | Symbolic link file (a file that points to another file) |
| Green | Executable file (a program) |


## Wildcaeds:
+ You can use file globbing (wildcards) to limit which files or directories you see.
+ For example, the `*` character can match "zero or more of any characters" in a filename.
+ Note that the `-d` option prevents files from subdirectories from being displayed.
+ ==It should always be used with the `ls` command when you are using file globbing.==
```bash
sysadmin@localhost:~$ ls -d /etc/s*                                           
/etc/securetty  /etc/sgml     /etc/shells  /etc/ssl        /etc/sysctl.conf   
/etc/security   /etc/shadow   /etc/skel    /etc/sudoers    /etc/sysctl.d      
/etc/services   /etc/shadow-  /etc/ssh     /etc/sudoers.d  /etc/systemd 
```
![[Screenshot from 2024-02-23 10-03-34.png]]


## `?` character:
+ The `?` character can be used to match exactly 1 character in a file name.
+ Execute the following command to display all of the files in the `/etc` directory that are exactly four characters long:
```bash
sysadmin@localhost:~$ ls -d /etc/????                 
/etc/bind  /etc/init  /etc/motd  /etc/perl  /etc/skel 
/etc/dpkg  /etc/ldap  /etc/mtab  /etc/sgml  /etc/udev 
```
```bash
am@ubuntu:/usr/share/doc$ ls -d a??
acl  apg  apt
```


## Square brackets:
+ By using square brackets `[ ]` you can specify a single character to match from a set of characters.
+ Execute the following command to display all of the files in the `/etc` directory that begin with the letters `a`, `b`, `c` or `d`:
```bash
ls –d /etc/[abcd]*
```