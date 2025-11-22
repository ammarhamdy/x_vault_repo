
It’s a classic Unix utility for displaying ==binary== file contents in human-readable forms (hex, octal, ASCII, interpreted integers, etc.)

# Basic view (canonical)
This is the simplest useful form (hex bytes + ASCII on the right):
```sh
hexdump -C image.png
```
Output columns:
- Left column: byte **offset** (hex).
- Middle: 16 bytes per line shown as hex pairs.
- Right: printable ASCII characters (non-print-ables shown as `.`).


# Limit output to the first N bytes:
```sh
hexdump -n 64 -C file.bin   # first 64 bytes only
```

# Skip bytes (start at offset):
```sh
hexdump -s 512 -n 64 -C file.bin   # show 64 bytes starting at offset 0x200
```

# Simple byte-oriented displays

Print every byte as a two-digit hex value, space-separated:
```sh
hexdump -v -e '1/1 "%02x "' file.bin
```

Print 16 bytes per line (grouped):
```sh
hexdump -v -e '16/1 "%02x " "\n"' file.bin
```
- `-v` prevents suppression of identical lines (GNU `hexdump` collapses repeated lines otherwise).
- `-e` supplies a custom format expression.

# Common short options:
- `-c` : print bytes as ASCII characters (with C-style escapes for non-print-ables).
- `-b` : print bytes as octal numbers.
- `-o` : print 2-byte units as octal.
- `-x` : print 2-byte units as hex.

---

# Interpreting multi-byte integers (format strings)

`hexdump -e` is powerful for interpreting groups of bytes as integers, floats, etc.

Print 32-bit (**4-byte**) words as 8-digit hex values (one word per line):
```sh
hexdump -v -e '4/4 "%08x\n"' file.bin
```
`4/4` means: read 4 items of 4 bytes each per output iteration (here it groups 4×4 = 16 bytes per line); the format prints each 4-byte item as `%08x` then newline.

Print 32-bit unsigned integers in decimal:
```sh
hexdump -v -e '4/4 "%u " "\n"' file.bin
```

Print single bytes in hex with ASCII on the side (custom canonical):
```sh
hexdump -v -e '16/1 "%02x " "  "  16/1 "%_p\n"' file.bin
```
`%_p` prints the corresponding character, like canonical `-C`.


---

# Examples

```sh
hexdump -c file.bin        # ASCII view with escapes
hexdump -b file.bin        # octal bytes
hexdump -x file.bin        # 2-byte hex words
```

```sh
hexdump -C file              # canonical hex + ASCII
hexdump -n 16 -C file        # first 16 bytes
hexdump -s 512 -n 64 -C file # 64 bytes at offset 0x200
hexdump -v -e '1/1 "%02x "' file    # bytes as hex, spaced
hexdump -v -e '16/1 "%02x " "\n"' file  # 16 bytes per line
hexdump -c file              # ASCII/C-escaped chars
dd if=file bs=1 skip=100 count=32 2>/dev/null | hexdump -C
```
