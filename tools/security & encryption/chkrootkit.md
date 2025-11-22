

https://www.kali.org/tools/chkrootkit/


```bash
sudo apt install chkrootkit
```

# Running chkrootkit
```bash
sudo chkrootkit
```


# Interpreting Output
The output will show a list of checks like:
```
Checking `bindshell'... not infected
Checking `lkm'... suspicious
```
- `not infected`: No signs of that rootkit
- `INFECTED`: Potential rootkit activity
- `suspicious`: Something unusual was found, might be benign but deserves attention

# Use with Options

**Verbose output:**
```bash
sudo chkrootkit -v
```

**Specify directory (e.g., for chroot):**
```bash
sudo chkrootkit -r /path/to/mounted/system
```

**Check specific test:**
```bash
sudo chkrootkit -t testname
```
Replace `testname` with the specific test (like `wted`, `re-entries`, `bindshell`, etc.)

