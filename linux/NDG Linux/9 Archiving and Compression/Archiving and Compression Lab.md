
`tar` stands for **T**ape **AR**chive. This command was originally used to create tape backups, but today it is more commonly used to create archive files.


To add a file to an existing archive, use the `-r` option to the `tar` command. Execute the following commands to perform this action and verify the existence of the new file in the `tar` archive:

```bash
tar -rvf udev.tar /etc/hosts
tar –tvf udev.tar
```


## `gzip` example:
+ When you use `gzip`, the original file is replaced by the zipped file. 
+ In the example above, the `words` file was replaced with `words.gz`.
+ When you unzip the file, the zipped file will be replaced with the original file.
```bash
cp /usr/share/dict/words .
ls -l words
gzip words
ls -l words.gz
```
+ To view the contents of a `zip` archive, use with the `-l` option with the `unzip` command:
```bash
unzip -l udev.zip
```

## `bzip2` example:
+ The compressed file is created with a `.bz2` extension. The extension is removed when uncompressed.
```bash
ls -l words
bzip2 words
ls -l words.bz2
```

