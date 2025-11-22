

## `&` (Background Execution)
Runs a command **in the background**, allowing the terminal to accept new commands immediately.
```sh
sleep 10 & echo "This runs immediately"
```
Check background jobs:
```sh
jobs
```
Bring a job to the foreground:
```sh
fg %1  # Brings job 1 back to foreground
```


## `&&` (Logical AND)
Runs the **second command only if** the first **succeeds** (exit status `0`).
```sh
mkdir new_folder && cd new_folder
```


## `||` (Logical OR)
Runs the **second command only if** the first **fails** (exit status **≠ 0**).
```sh
mkdir existing_folder || echo "Folder already exists"
```


## `|` (Pipe Operator)
Sends the **output** of one command as **input** to another.
```sh
ls -l | grep ".txt"
```


## Combining Separators
```sh
mkdir test_dir && cd test_dir || echo "Failed to create or enter directory"
```