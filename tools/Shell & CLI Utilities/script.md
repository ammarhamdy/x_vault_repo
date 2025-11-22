

`script` command is a utility that **records everything you type and everything that appears on your terminal** into a file (a “typescript”).

# How it works:

By default, it creates a file called `typescript` in the current directory.

It logs **both your commands and their output** until you exit.

You stop recording by typing:
```sh
exit
```


# Start recording:
```sh
script
```
Creates a file named `typescript` with your session inside.

# Record to a custom file:

```sh
script my_log.txt
```
Saves everything into `my_log.txt`.

```sh
script -a my_log.txt
```
Append to an existing log file.


