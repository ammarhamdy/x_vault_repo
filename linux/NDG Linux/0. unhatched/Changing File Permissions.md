

## `chmod` command:
+ Only the root user or the user who owns the file is able to change the permissions of a file.


## Why is the command named `chmod` instead of `chperm`?
+ Permissions used to be referred to as modes of access, so the command `chmod` really means **ch**ange the **mod**es of access.


## Two techniques Change the modes:
+ There are two techniques for changing permissions with the `chmod` command: symbolic and octal.
+ The symbolic method is good for changing one set of permissions at a time. The octal or numeric method requires knowledge of the octal value of each of the permissions and requires all three sets of permissions (user, group, other) to be specified every time.


### The Symbolic Method:
```
chmod [<SET><ACTION><PERMISSIONS>]... FILE
```
+ To use the symbolic method of `chmod` first indicate which set of permissions is being changed:

| Symbol | Meaning                                                                |
| ------ | ---------------------------------------------------------------------- |
| `u`    | User: The user who owns the file.                                      |
| `g`    | Group: The group who owns the file.                                    |
| `o`    | Others: Anyone other than the user owner or member of the group owner. |
| `a`    | All: Refers to the user, group and others.                             |
+ Next, specify an action symbol:
```
chmod [<SET><ACTION><PERMISSIONS>]... FILE
```

| Symbol | Meaning                             |
| ------ | ----------------------------------- |
| `+`    | Add the permission, if necessary    |
| `=`    | Specify the exact permission        |
| `-`    | Remove the permission, if necessary |
+ After an action symbol, specify one or more permissions to be acted upon.
```
chmod [<SET><ACTION><PERMISSIONS>]... FILE
```

| Symbol | Meaning |
| ------ | ------- |
| `r`    | read    |
| `w`    | write   |
| `x`    | execute |


