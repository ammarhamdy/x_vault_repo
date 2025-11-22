

# Instillation
```sh
sudo apt install poppler-utils
```


# Extract images from a PDF:
```sh
pdfimages -all input.pdf output_prefix
```
- `input.pdf` → your PDF file.
- `output_prefix` → prefix for extracted images (e.g., `img` will produce `img-000.jpg`, `img-001.png`, etc.).
- `-all` → keeps original formats (`JPEG`, `JP2`, etc.) without converting them.

