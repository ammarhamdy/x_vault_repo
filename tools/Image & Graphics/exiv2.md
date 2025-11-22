
https://www.kali.org/tools/exiv2/

---

`exiv2` is a command-line utility and C++ library to manage image metadata, such as `EXIF`, `IPTC`, and `XMP`.

```bash
sudo apt install exiv2
```

---

# View metadata:
```bash
exiv2 image.jpg
```

# Extract all metadata:

```bash
exiv2 -pa image.jpg
```

```bash
for i in *; do if [ -f "$i" ]; then exiv2 -ps "$i"; echo -e "\n\n"; fi; done
```

# Modify metadata (e.g., set Author):
```bash
exiv2 -M"set Exif.Image.Artist JohnDoe" image.jpg
```

# Remove all metadata:
```bash
exiv2 rm image.jpg
```

# Rename files based on metadata 
like capture date:
```bash
exiv2 rename image.jpg
```

# Example Use Case
Suppose you want to change the timestamp on a photo:
```bash
exiv2 -M"set Exif.Photo.DateTimeOriginal 2023:01:01 12:00:00" photo.jpg
```


---

# Image metadata (`EXIF`, `IPTC`, `XMP`)?

**Image metadata** is **information embedded within a digital image file** that describes details about the image, such as:
- When it was taken
- What camera was used
- Camera settings (exposure, aperture, ISO, etc.)
- GPS coordinates
- Author/creator info
- Copyright status
- Editing history

## `EXIF` (Exchangeable Image File Format)

**Mainly used by cameras and smartphones.**
### Common `EXIF` fields:
- **Camera model and make**
- **Date and time taken**
- **Shutter speed, aperture, ISO**
- **Focal length**
- **GPS location** (if enabled)

## `IPTC` (International Press Telecommunications Council)

**Used primarily by photojournalists and media professionals.**
### Common `IPTC` fields:
- **Author/photographer name**
- **Copyright info**
- **Title and caption**
- **Keywords and categories**

## `XMP` (Extensible Metadata Platform)

**An Adobe-developed format that's flexible and XML-based.**
- Often used by **`Lightroom`**, **Photoshop**, and **other editing software**
- Can include all `EXIF` and `IPTC` fields plus custom tags
- Stores data in a way that survives editing (non-destructive)