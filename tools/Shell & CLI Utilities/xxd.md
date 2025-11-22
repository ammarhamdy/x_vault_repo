
**Shows hexadecimal representation**
```
xxd image.jpg  
```

# First line on file
```sh
xxd 5651960.jpg | head -n 1
```

# Human-friendly hex
```sh
xxd -l 16 -g 1 image.png
```
- `-l 16` limits output to the first 16 bytes.
- `-g 1` groups output by single bytes.

# Plain continuous hex

```sh
xxd -l 16 -p image.png
```

```sh
head -c 16 image.png | xxd -p
```

