
`du` stands for **disk usage**.

It’s a Unix/Linux command that estimates and reports the amount of disk space used by files and directories.

By default, it shows the space each subdirectory consumes:
```bash
du /path/to/dir
```

With `-h` (human-readable), you get sizes in KB/MB/GB instead of just blocks:
```bash
du -h /path/to/dir
```

 With `-s` (summary), you get only the total size:
```bash
du -sh /path/to/dir
```

To see **all subdirectories** with their sizes:
```sh
du -h --max-depth=1 /path/to/dir
```