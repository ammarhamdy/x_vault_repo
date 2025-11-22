
# Hiding Secret Text Inside an Image File

## Append a hidden message to the end of a `.jpg` file.

JPEG decoders ignore extra stuff at the end, so the picture still opens normally — but the hidden text is still there.

```python
# Step 1: Pick an image
with open("example.jpg", "rb") as f:
    data = f.read()

# Step 2: Add a secret message
secret_message = "TOP_SECRET: Mohamed was here!"
secret_bytes = secret_message.encode("utf-8")

# Step 3: Combine original + secret
combined = data + b"SECRETSTART" + secret_bytes + b"SECRETEND"

# Step 4: Save as a new image
with open("hidden.jpg", "wb") as f:
    f.write(combined)
```
Extract Data
```python
# Step 1: Read file
with open("hidden.jpg", "rb") as f:
    data = f.read()

# Step 2: Find markers
start = data.find(b"SECRETSTART") + len(b"SECRETSTART")
end = data.find(b"SECRETEND")

# Step 3: Extract
hidden_message = data[start:end].decode("utf-8")
print("Hidden message:", hidden_message)
```


## Hiding text _inside the pixels_ of an image.

This is called **LSB steganography (Least Significant Bit)**, and it’s one of the most classic tricks.

### How it works
- Each pixel in an image has **RGB values** (Red, Green, Blue), usually from `0–255` → stored in 8 bits each.
- Example:
    - Pixel red value = `10110010` (binary = 178).
    - Change the **last bit** → `10110011` (binary = 179).
- To the human eye: 178 and 179 look the same (almost no color difference).
- But that last bit can store part of a secret message.

So by changing the least significant bits across many pixels, we can hide data **invisible to humans**.


## Hide the message across all 3 channels (R, G, B)


```python
from PIL import Image

def hide_message(image_path, output_path, secret_message):
    # Open image
    img = Image.open(image_path)
    img = img.convert("RGB")
    pixels = img.load()

    # Convert message to binary
    binary_message = ''.join(format(ord(c), '08b') for c in secret_message)
    binary_message += '1111111111111110'  # End marker

    msg_index = 0
    for y in range(img.height):
        for x in range(img.width):
            if msg_index >= len(binary_message):
                break

            r, g, b = pixels[x, y]
            rgb = [r, g, b]

            # Hide 1 bit in each channel
            for channel in range(3):
                if msg_index < len(binary_message):
                    rgb[channel] = (rgb[channel] & ~1) | int(binary_message[msg_index])
                    msg_index += 1

            pixels[x, y] = tuple(rgb)

    img.save(output_path)
    print("✅ Secret hidden in", output_path)

# Example usage
hide_message("example.png", "stego.png", "Mohamed is learning deep steganography!")

```

```python
def extract_message(stego_path):
    img = Image.open(stego_path)
    img = img.convert("RGB")
    pixels = img.load()

    binary_message = ""
    for y in range(img.height):
        for x in range(img.width):
            r, g, b = pixels[x, y]
            binary_message += str(r & 1)
            binary_message += str(g & 1)
            binary_message += str(b & 1)

    # Split into 8-bit chunks → chars
    chars = [binary_message[i:i+8] for i in range(0, len(binary_message), 8)]
    message = ""
    for c in chars:
        if c == "11111110":  # End marker
            break
        message += chr(int(c, 2))
    return message

# Example usage
print("🔎 Hidden message:", extract_message("stego.png"))

```

- A `1920×1080` image has about **2 million pixels**.
    
- With 3 bits per pixel → **~6 million hidden bits** = ~750 KB of secret text/data!