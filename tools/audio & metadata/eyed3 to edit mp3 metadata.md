

```sh
sudo apt install eyed3
```


----

# Show all tags of an MP3 file:
```sh
eyeD3 song.mp3
```

# Set title, artist, album:
```sh
eyeD3 --title "My Song" --artist "The Artist" --album "The Album" song.mp3
```

# Set genre, track number, year:
```sh
eyeD3 --genre "Rock" --track 5 --release-date 2023 song.mp3
```

# Add album art (cover image):
```sh
eyeD3 --add-image cover.jpg:FRONT_COVER song.mp3
```
You can use these image types:
- `FRONT_COVER`
- `BACK_COVER`
- `LEAD_ARTIST`
- `ARTIST`
- `ILLUSTRATION`
- etc.

# Remove all tags:
```sh
eyeD3 --remove-all song.mp3
```

# `eyeD3` --remove-all-images 
```sh
eyeD3 --remove-all-images yourfile.mp3
```

# Loop over all MP3 files
```sh
for f in *.mp3; do
    echo "Processing: $f"
    eyeD3 --remove-all-images "$f"
done
```

---
# Use `eyeD3` in Python scripts

```python
import eyed3

audiofile = eyed3.load("song.mp3")
audiofile.tag.title = "New Title"
audiofile.tag.artist = "New Artist"
audiofile.tag.album = "New Album"
audiofile.tag.save()
```