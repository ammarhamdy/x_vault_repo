
## The `su` Command:
```
su OPTIONS USERNAME
```
+ The `su` command allows you to temporarily act as a different user. 
+ ==It does this by creating a new shell. ==
+ By default, if a user account is not specified, the `su` command will open a new shell as the root user, which provides administrative privileges.


## The Shell is:
+ The shell is simply a text input console that lets you type in commands.


## The `sudo` Command:
```
sudo [OPTIONS] COMMAND
```
+ The `sudo` command allows a user to execute a command as another user ==without creating a new shell.==
+ Instead, to execute a command with administrative privileges, use it as an argument to the `sudo` command.
+ Like the `su` command, the `sudo` command assumes by default the `root` user account should be used to execute commands.


