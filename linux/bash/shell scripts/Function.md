

# shell functions:
+ Shell functions are “mini-scripts” that are located inside other scripts and can act as autonomous programs.
+ Shell functions have two syntactic forms.
+ A function must contain at least one command.
+ A `return` command is optional. 
+ Shell function names follow the same rules as variables.
```
function name {
	commands
	return
}
```

```
name (){
	commands
	return
}
```

```bash
#!/bin/bash
# Shell function demo

function step2 {
 echo "Step 2"
 return
}

 # Main program starts here
 echo "Step 1"
 step2
 echo "Step 3"
```


#### Local variable:
+ Local variables are accessible only within the shell function in which they are defined and cease to exist once the shell function terminates.
+ Having local variables allows the programmer to use variables with names that may already exist, either in the script globally or in other shell functions


---

# Common error

```
function: not found
```
means your shell interpreter is not recognizing the function keyword. 

This typically happens if:
You're running the script with `sh` (POSIX shell), not `bash`.

Or you're executing the script on a system where sh is a minimal shell (like BusyBox or Alpine Linux), which doesn’t support Bash-specific syntax like function.

when run script like:
```bash
function play {
	 echo "play."
}
```
use bash not sh:
> bash play

---

**return value from function** 
```bash
get_greeting() {
  local name=$1
  echo "Hello, $name!"
}

greeting=$(get_greeting "Alice")
echo "$greeting"
```


