
The `find` command on Ubuntu (and more generally, in Linux/Unix systems) is a **powerful tool** for searching files and directories in a filesystem hierarchy. 

It can locate files based on name, type, size, permissions, modification time, ownership, and more.

```sh
find [path] [options] [expression]
```
- **path** → where to start searching (`/`, `.`, `/home/user`, etc.)
- **options/expression** → rules that filter results (e.g., name, type, size)
- **action** → what to do with matches (default is to print their paths)

# Search by file name
```sh
find /home -name "file.txt"
```

# Search by file type

**Finds all files in `/var/log`**
```sh
find /var/log -type f
```

**Finds all directories starting from current directory**
```sh
find . -type d
```

**Finds all symbolic links**
```sh
find / -type l
```

# Search by size

**Finds files larger than 100 MB**
```sh
find / -size +100M
```

**Finds files smaller than 10 KB**
```sh
find / -size -10k
```

# Search by time

**Files modified in the last 7 days**
```sh
find /home -mtime -7
```

**Files last accessed more than 30 days ago**
```sh
find /var/log -atime +30
```

# Execute commands on found files

**Deletes all `.log` files in current directory and subdirectories**
```sh
find . -name "*.log" -exec rm {} \;
```
`{}` = placeholder for each file
`\;` ends the command

**Shows sizes of all `.log` files**
```sh
find /var/log -type f -name "*.log" -exec du -h {} \;
```

**Searches for `keyword` inside `.conf` files efficiently (`+` is faster than `\;`)**
```sh
find /etc -type f -name "*.conf" -exec grep "keyword" {} +
```

# Combine conditions

**Finds files ending with `.sh` **or** `.py`**
```sh
find / -type f \( -name "*.sh" -o -name "*.py" \)
```

**Finds files larger than 10 MB modified in the last 30 days**
```sh
find /home -type f -size +10M -mtime -30
```

**Combine with `xargs` for performance in bulk operations**
```sh
find . -name "*.tmp" -print0 | xargs -0 rm
```

# Stop recursive search

By default, `find` **recursively** searches into all subdirectories.  
If you only want to search in the **current directory (non-recursive)**, you can limit the depth:

**Use `-maxdepth`**
```sh
find . -maxdepth 1 -name "*.txt"
```
- `-maxdepth 1` → only look in the current directory.
- `-name "*.txt"` → find all `.txt` files.

**Combine with `-mindepth`**
```sh
find . -mindepth 1 -maxdepth 1 -type f
```
- `-mindepth 1` → exclude the current directory itself (`.`).
- `-maxdepth 1` → do not go into subdirectories.
- `-type f` → only files (not directories).

