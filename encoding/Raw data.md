![[Pasted image 20250820102934.png]]

At the lowest level, **all files are indeed just `0s` and `1s`** (binary). 
For example:
```
00101101 01101001 01101101 01100001 01100111 01100101
```
But if computers always showed you raw binary, it would be unreadable for humans.
That’s why you see those “weird characters” (`ÿØÿà JFIF...`) instead of a wall of `0` and `1`.


Here’s why:

**Binary → Encoded Text**
    - Computers group 8 bits (like `01001010`) into a **byte**.
    - Each byte can be mapped to a symbol using a character set (like ASCII or extended Latin).
    - Example: `01001010` = decimal 74 → letter **J**.

**Image Raw Data**
- A JPEG image starts with bytes like `11111111 11011000` (binary).
- Instead of showing `11111111 11011000`, your computer (or web browser) tries to interpret those bytes as characters.
- That’s why you see `ÿØ` (special characters) instead of `11111111 11011000`.

**Why not just 0s and 1s?**
- Because raw binary is huge and unreadable.
- Showing it as “characters” is more compact and sometimes gives hints (like `JFIF` at the start of a JPEG, which tells us “this is a JPEG file”).


----
# Convert raw file data to binary


```python
# Read a file in binary mode
with open("example.jpg", "rb") as f:
    raw_bytes = f.read()

# Convert first 20 bytes into binary representation
binary_data = ' '.join(format(byte, '08b') for byte in raw_bytes[:20])

print(binary_data)
```
You probably don’t want to print the _whole file_, because an image can be millions of bytes!


----
# Convert binary raw file data

```python
binary_string = "01001010 01000110 01001001 01000110"  # Example bits = "JFIF"

# Split and convert each group of 8 bits into a byte
bytes_data = bytes(
	int(b, 2) for b in binary_string.split()
)

# Save back into a file
with open("reconstructed.jpg", "wb") as f:
    f.write(bytes_data)
```

## bytes

**`bytes`** is a built-in type and also a constructor (like `int()` or `str()`).  
It represents a **sequence of raw bytes**

```python
data = bytes([65, 66, 67])
print(data)        # b'ABC'
print(list(data))  # [65, 66, 67]
```
Each integer is turned into its binary (8-bit) form.

**If you give it just an integer `n`**  
It makes a bytes object of length `n`, filled with zeros.
```python
zeros = bytes(5)
print(zeros)       # b'\x00\x00\x00\x00\x00'
```


---
# Hex

```python
python3 - <<'PY'
fn = "image.png"
n = 16
b = open(fn,"rb").read(n)
print(b.hex())
PY
```
Or an alternate Python line that prints space-separated byte hex pairs:
```python
python3 - <<'PY'
fn="image.png"; n=16
b=open(fn,"rb").read(n)
print(" ".join(f"{x:02x}" for x in b))
PY
```
## Recognizing format from first bytes
- PNG magic (first 8 bytes): `89 50 4e 47 0d 0a 1a 0a`
- JPEG magic (first 3 bytes): `ff d8 ff`

So if you run `xxd -l 8 -g 1 image.png` and see `89 50 4e 47 0d 0a 1a 0a` you have a PNG.

