
The **`timeout`** command in Ubuntu (and most Linux systems) is used to **run a command with a time limit**. If the command doesn’t finish within the specified time, `timeout` will stop (kill) it.

# Syntax
```sh
timeout [OPTION] DURATION COMMAND [ARG]...
```
- **DURATION** → Time limit (e.g., `10s`, `5m`, `2h`).
- **COMMAND** → The command you want to run.

# Example

## Run `ping` for 5 seconds
```sh
timeout 5s ping google.com
```
## Run a script with a **1-minute limit**
```sh
timeout 1m ./long_script.sh
```

# Use `--signal` to specify what signal to send (default is `SIGTERM`)
```sh
timeout --signal=SIGKILL 10s my_command
```
 `--signal` to specify what signal to send (default is `SIGTERM`):
To check exit codes:
- `124` → Command timed out
- `137` → Killed with `SIGKILL`
- Other → Exit code of the command itself


# Python’s `pty` Module

The Python `pty` module emulates the functionality of a physical terminal device. 

In the following example, we upgrade a Python shell to a fully interactive `TTY` bash shell by using the `pty.spawn()` function.
```python
import pty
pty.spawn("/bin/bash")
```

On a compromised host with Python installed, you could elevate your
shell by executing the following command:
```python
python3 -c 'import pty; pty.spawn("/bin/bash")'
```