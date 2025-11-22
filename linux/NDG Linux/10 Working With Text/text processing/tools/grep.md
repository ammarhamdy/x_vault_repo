The `grep` command is used in Linux/Unix to **search for text patterns** inside files or output. 

```sh
grep [options] pattern [file...]
```


----

# Useful Options Summary

| Option | Description                             |
| ------ | --------------------------------------- |
| `-i`   | Ignore case                             |
| `-r`   | Recursive search                        |
| `-n`   | Show line numbers                       |
| `-l`   | Show filenames only                     |
| `-c`   | Count matches                           |
| `-v`   | Invert match (show non-matches)         |
| `-E`   | Use extended regex                      |
| `-o`   | show only the matched parts of the line |

**Ignore case**
```sh
grep -i "error" logfile.txt
```

**Show line numbers**
```sh
grep -n "error" logfile.txt
```

**Search recursively in all files in a folder**
```sh
grep -r "password" /etc/
```

**Count matches**
```sh
grep -c "404" access.log
```

**Show only filenames with matches**
```sh
grep -l "admin" *.txt
```

**Match IP addresses**
```sh
grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" scan.txt
```

```sh
grep -oE "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" random-hosts.txt
```

**Stricter IP address validation** 
```sh
grep -oE '\b((25[0-5]|2[0-4][0-9]|1?[0-9]?[0-9])\.){3}(25[0-5]|2[0-4][0-9]|1?[0-9]?[0-9])\b'
```

**Match newline**

Use `grep -Pzo` (Perl-compatible regex + null-separated output)
```sh
grep -Pzo '"id": "[a-z0-9-]+",.*?"' file.json
```
- `-P` → enables Perl regex (PCRE)
- `-z` → treats the entire input as a single line, replacing newlines with `\0` (so `.` matches across lines)
- `-o` → prints only the match
- `.*?` → non-greedy match (Perl-style)

If `grep -P` doesn’t support `-z` on your system, use:
```sh
pcregrep -M '"id": "[a-z0-9-]+",.*?"' file.json
```