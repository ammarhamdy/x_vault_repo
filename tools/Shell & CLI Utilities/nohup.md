
The `nohup` command in Unix/Linux stands for **"no hang up"**.

**Prevents a process from being terminated when you close the terminal or log out.**

It **ignores the SIGHUP (hangup) signal**, which is normally sent to processes when their terminal closes.

Commonly used to **run long-running commands in the background**, especially on remote servers.


**Basic Syntax:**
```bash
nohup command [arguments] &
```

**Example:**
```bash
nohup jmeter -n -t test.jmx -l result.jtl > jmeter.log 2>&1 &
```
- `>` → Redirects standard output to `jmeter.log`
- `2>&1` → Redirects standard error to the same file

**To See Running Process:**
```bash
ps aux | grep jmeter
```

**To Stop It:**
```bash
kill <PID>
```