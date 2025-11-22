

## About `su`:
+ There is some confusion as to what the initials “su” stand for (==substitute user==, ==switch user==, and ==superuser== are all often referenced) , but the main thing to note is that it allows an administrator to change their login to any user on the system.


## `sudo` live time:
+ The `sudo` command is typically used to execute a single command as the root user by prefixing that command with `sudo`. 
+ The `sudo` command must be configured by the root user before an ordinary user can use it.
+ By default, the `sudo` command ==stays in effect for 15 minutes== on Ubuntu systems where the root account is not enabled by default.


## Return bask to original user:
+ After using the shell started by the `su` command to perform the necessary administrative tasks, return to your original shell (and original user account) by using the `exit` command. 
+ Confirm the user identity change using the `id` command.



----
# User Accounts


User and system accounts are defined in the `/etc/passwd` and `/etc/shadow` files.
View the first ten lines from the `/etc/passwd` file. 
While the `passwd` file contains general information about a user such as username, UID, GID, home directory and login shell, the modern `shadow` file has additional details including encrypted password and password policy



----
# Passwords


The `/etc/shadow` file contains information about users’ passwords.
Try to view the first few lines of `/etc/shadow` file, a file that contains users' encrypted passwords and information about aging them


## `getent` command: 
+ Another way to retrieve the account information for a user is by running the following command: `getent passwd username`. 
+ The `getent` command has the advantage over the `grep` command as it is also able to access user accounts that are not defined locally. 
+ In other words, the `getent` command is able to get user information for users who may be defined on network directory servers such as LDAP, NIS, Windows Domain, or Active Directory Domain servers.
+ Use the `getent` command to retrieve the information about the sysadmin:
```
getent passwd sysadmin
```


## Group information come from:
+ The file `/etc/group`, together with `/etc/passwd`, determines your group memberships. 
+ Your default primary group is determined by matching your GID found in `/etc/passwd` to the GID defined for a group in the `/etc/group`.
+ Any secondary group memberships are defined in the `/etc/group` file.
+ The format of entries in the `/etc/group` file for each line is:
```
group_name:password:GID:user_list
```



----
# Who is On the System


## `who` command:
+ Use the `who` command to get the current list of users on the system: 
	+ Username:
		+ This column indicates the name of the user who is logged in.
	+ Terminal:
		+ This column indicates which terminal window the user is working in.
	+ Date:
		+ This column indicates when the user logged in.
	+ Host:
		+ Although there is no output for the fourth column in this case, it can be the name or IP address of a local or remote host.


## `w` command:
+ Use the `w` command to get a more detailed view of the users who are currently on your system
+ Output from the `w` command displays a summary of how long the system has been running, how many users are logged in and the system load averages for the past 1, 5, and 15 minutes.
+ Also displayed is an entry for each user with their login name, tty name (terminal name), host, login time, idle time, JCPU (CPU time used by background jobs), PCPU (CPU time used by the current process) and what is executing on the current command line.



---
# Viewing Login History


The `last` command reads the entire login history from the `/var/log/wtmp` file and displays all logins and reboot records by default.

The `last` command to view the `/var/log/wtmp` file which keeps a log of all users who have logged in and out the system.



----

The `/etc/group` file follows what structure?
```
group_name:password_placehoder:GID:user_list
```

Here’s a sample entry in the `/etc/group` file:
```
mygroup:x:1001:user1,user2,user3
```
- **`mygroup`**: Group name.
- **`x`**: Empty password field.
- **`1001`**: Group ID.
- **`user1,user2,user3`**: List of users who belong to this group.


