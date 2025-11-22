
Steganography is the practice of concealing إخفاء a secret message within another message or physical object in a way that the presence of the hidden message isn't apparent.

The word comes from the Greek words **"steganos"** (covered or hidden) and **"graphein"** (writing), literally meaning "covered writing." Unlike cryptography, which scrambles a message to make it unreadable, steganography's goal is to hide the very existence of the message itself.


# How Steganography Works

In the digital world, steganography is often used with media files like images, audio, and video. 

These files are ideal for hiding information because they contain a large amount of data that can be slightly altered without noticeable changes. 

A common technique is **Least Significant Bit (LSB) steganography**.

This method involves embedding the secret information into the least significant bits of a file. In an image, for example, each pixel is made up of bits that represent color. By changing the last bit of a pixel's color value, you can hide a bit of data. The change is so minimal that the human eye can't detect any difference in the image's appearance. The secret message is then reconstructed by a recipient who knows where to look.

## Steganography can also be used in other ways, such as:

- **Text Steganography:** Hiding a message by manipulating the formatting of a text file, such as changing the spacing between words or lines.
    
- **Audio Steganography:** Embedding a message into an audio file by altering the binary sequence. This can be done by changing the least significant bits of the audio data.
    
- **Network Steganography:** Hiding information within network traffic, such as in TCP/IP headers or payloads.

----
# Popular steganography algorithms


## Image Steganography

1. **LSB (Least Significant Bit)**
    - The most common and simple method.
    - Hides secret data in the least significant bits of pixel values.
    - Example: If a pixel’s RGB value is `(10110010)`, changing the last bit won’t affect its appearance much.
        
2. **LSB Matching (±1 embedding)**
    - A variation of تنوع في LSB.
    - Instead of flipping the last bit directly, it increments/decrements pixel values by 1 to match the hidden data.
        
3. **DCT (Discrete Cosine Transform) Steganography**
    - Used in JPEG images.
    - Data is embedded in the frequency domain by modifying DCT coefficients instead of pixel values.
        
4. **Spread Spectrum**
    - Distributes hidden data across the whole image like noise.
    - Harder to detect because it mimics natural noise patterns.
        
5. **Masking & Filtering**
    - Similar to watermarking.
    - Embeds information in significant areas of an image, like edges or textures.
        

## Audio Steganography

1. **LSB in Audio Samples**
    - Similar to image LSB, but hides data in digital audio samples.
        
2. **Echo Hiding**
    - Hides data by introducing short echoes into an audio file.
    - The delay between original and echoed signal represents bits.
        
3. **Phase Coding**
    - Modifies the phase of audio signals to encode data.
    - Hard for humans to detect.
        
4. **Spread Spectrum Audio**
    - Similar to spread spectrum in images, spreads hidden bits across audio frequencies.

## Video Steganography

- Combines **image + audio steganography**.
    
- Data can be hidden in:
    - Frame images (using LSB/DCT).        
    - Audio track (echo hiding, phase coding).
    - Motion vectors in compressed video (e.g., MPEG).

## Text Steganography

1. **Whitespace Encoding**
    - Extra spaces, tabs, or line breaks represent binary data.

2. **Font or Character Substitution**
    - Replace letters with visually similar Unicode characters (e.g., `a` vs `а` in Cyrillic).

3. **Syntactic Methods**
    - Vary punctuation or grammar to encode data.

4. **Semantic Methods**
    - Replace words with synonyms according to a predefined mapping.

## Modern Advanced Algorithms

- **F5 Algorithm**: Hides data in JPEG images by modifying DCT coefficients while reducing statistical detectability.

- **OutGuess**: Preserves statistics of the cover file, making detection harder.

- **WOW (Wavelet Obtained Weights)**: Uses wavelet transforms to minimize detectable distortions.

- **HUGO (Highly Undetectable SteGO)**: Uses machine-learning-like cost functions to choose best embedding positions.


----
# Tools for Steganography

- **`Steghide`:** A popular command-line tool that can embed data into various file types, including JPEG and WAV files, and offers encryption for the hidden data.
    
- **`OpenStego`:** An open-source tool with a graphical interface that allows you to hide data in images and apply digital watermarks.
    
- **`ExifTool`:** While primarily a metadata editor, it can be used to view and manipulate the metadata of a file, where hidden information might be stored.
    
- **`Binwalk`:** A tool used to search binary files for embedded files and executable code, which can help in finding hidden data within firmware or other file types.
    
- **`Sonic Visualizer`:** This tool is for audio analysis but can be used to detect hidden images within audio files by analyzing the spectrogram


