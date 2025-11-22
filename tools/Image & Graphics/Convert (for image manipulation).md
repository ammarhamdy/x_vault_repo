
One of the most powerful image manipulation tools in Linux, and it comes from the **`ImageMagick`** suite.

 **What is `convert`?**
- A command-line tool from **`ImageMagick`**.
- Lets you **create, edit, and transform images**. 
- Works with almost every format: `PNG`, `JPG`, `GIF`, `TIFF`, `PDF`, `SVG`, etc.

**Important note**
In newer versions of `ImageMagick (v7+)`, `convert` is **renamed to `magick`**. 
So instead of: `convert input.png output.jpg`
you’d use: `magick input.png output.jpg`

---

# Create a new image

```sh
convert -size 200x200 canvas:red red.png
```

```sh
convert -size 300x300 canvas:"#FF5733" output.png
```

# Resize an image
```sh
convert input.jpg -resize 300x300 output.jpg
```

# Change format
```sh
convert input.png output.jpg
```

# Grayscale (remove color)
```sh
convert input.jpg -colorspace Gray output.jpg
```

# Crop
```sh
convert input.jpg -crop 200x200+10+10 cropped.jpg
```

# Add text
```sh
convert input.jpg -pointsize 36 -fill white -annotate +50+100 "Hello!" output.jpg
```

# Combine multiple images
```sh
convert image1.jpg image2.jpg +append combined.jpg
```
Stitches images side by side.  
Use `-append` for vertical.


# Random gradient with `convert`

## Horizontal gradient (random start/end colors)
```sh
convert -size 800x600 gradient:"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))"-"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))" random_gradient.png
```

## Vertical gradient
```sh
convert -size 800x600 gradient:"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))"-"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))" -rotate 90 random_gradient_vert.png
```

## Diagonal (top-left → bottom-right)
```sh
convert -size 800x600 gradient:"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))"-"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))" -distort SRT 45 random_gradient_diag.png
```

## Radial gradient** (center outwards):
```sh
convert -size 800x600 radial-gradient:"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))"-"rgb($(shuf -i0-255 -n1),$(shuf -i0-255 -n1),$(shuf -i0-255 -n1))" random_radial.png
```