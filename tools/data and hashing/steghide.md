
https://www.kali.org/tools/steghide/

---

`Steghide` is a **steganography tool** used to hide data within other files, such as images or audio files, without significantly altering the appearance or sound of the carrier file. 

It’s commonly used in security, digital forensics, and Capture The Flag (`CTF`) challenges.

```sh
sudo apt install steghide
```

For docs
```sh
sudo apt install steghide-doc
```
After installing, you can usually find the docs in: `/usr/share/doc/steghide-doc/`

---
# What `Steghide` Does

- **Embedding**: You can embed a secret file (like a text, archive, or another image) inside a carrier file (like a `.jpg`, `.bmp`, `.wav`, or `.au` file).

- **Extracting**: You can later retrieve the hidden file using the same tool.

- **Encryption**: The embedded data can be encrypted with a passphrase for security.

**Note**: Steghide only works with specific formats (JPEG, BMP, WAV, AU). For PNG or GIF files, you’ll need other tools (like `zsteg` or `pngcheck`).

---

# Embed a file
```sh
steghide embed -cf cover.jpg -ef secret.txt
```
- `-cf` → cover file (carrier)
- `-ef` → embedded file (secret)
- It will prompt you for a passphrase.

# Extract a file
```sh
steghide extract -sf cover.jpg
```
+ `-sf` → stego file (the file that contains hidden data)

# Info about a file
```sh
steghide info cover.jpg
```
Shows whether the file possibly contains embedded data.


