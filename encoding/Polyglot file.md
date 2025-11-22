
A **polyglot file** is a single file that is simultaneously valid in two (or more) different formats, depending on how you open or interpret it.

Polyglot files are a fascinating مبهر kind of file that different applications interpret in different ways.

A polyglot file works because many file formats are **forgiving**: parsers often ignore extra bytes, search for signature blocks in particular places, or accept optional sections. 

One way to create polyglot files is by manipulating the **file headers**, also ==known as file signatures or magic bytes==, found at the beginning of the file.

To make a file valid under two formats you arrange bytes so **both parsers find what they expect** while ignoring the other format’s extra data.


# Key Ideas

- **Format flexibility**: Because many file formats have optional headers, padding, or loose validation, it’s possible to structure a file so multiple parsers accept it.
    
- **Multiple valid interpretations**: For example, the same bytes could be read as both an **image (PNG)** and a **ZIP archive**, depending on which program opens it.


# Key techniques:

- **Concatenation** — put Format B’s bytes after Format A’s bytes when Format A’s parser ignores trailing garbage. (Very common with image+archive pairs.)
    
- **Header overlap** — craft the beginning of the file so it simultaneously satisfies both formats’ header requirements.
    
- **Dual header placement** — some formats put essential location/metadata at the end (e.g., ZIP central directory). That allows you to hide one format at the tail while an image reader still displays the image.
    
- **Trick parsers with comments/metadata sections** — embed one format inside a comment block or metadata field of the other (e.g., inserting text into an image’s metadata that is actually a different file).
    
- **Whitespace / language compatibility** — for code polyglots, exploit syntax shared across languages (e.g., comments, string delimiters) so the same source is valid for two interpreters.


# Examples

- **Image + ZIP hybrid**
    - You can append a ZIP archive to the end of a JPEG or PNG file.
    - Image viewers display it normally, but unzip tools can also extract files.
    - ZIP files locate their central directory near the **end** of the file, so if you append a ZIP file to an image, unzip tools can still find and extract the archive.
    - Result: open in an image viewer → see the picture. Open with an unzip tool → read the ZIP contents.

- **PDF + HTML hybrid**
    - A crafted file can be opened in a PDF reader as a document, but in a browser as a working HTML/JavaScript page.
    - Some PDF readers will tolerate extra data or can be tricked by placing PDF header and objects so the file remains a valid PDF, while a browser may interpret the file as HTML if the HTML portion is placed at the start or in a way the browser favors.

- **Code polyglots**
	- Keep to constructs understood by both languages (shared comment syntax, string quoting, no incompatible keywords).
    - A `.php` file that is also valid JavaScript or Perl depending on how it’s executed.       
    - Used in CTF challenges and obfuscation.
    - For example, small scripts can be written so they run in both language interpreters by placing language-specific parts inside comments or conditional blocks that one interpreter ignores.


# Important constraints — what you must satisfy for both formats

- **Headers & magic numbers**: At least one parser must find the required signature (magic number) where it expects it.
    
- **Position of metadata**: If a format needs data at the beginning or at a particular offset, the polyglot must respect that.
    
- **Checksums & lengths**: Some formats verify lengths or checksums — you must not break those checks (or choose formats that don’t enforce them strictly).
    
- **Parser tolerance**: Success depends on how strict each parser/validator is. Parsers differ across implementations.


# How defenders detect and mitigate polyglot abuse (useful if you’re learning security)

## Content-based validation: 
 Don’t rely solely on filename extensions; inspect file headers and check consistency between declared type and content.
## Strict parsing / sandboxing: 
Run file processors in isolated sandboxes or use robust file libraries that reject files with unexpected trailing data.
## Whitelist accepted structures: 
Validate that the file matches the exact structure you expect (not just a leading signature).
## Strip extraneous data: 
Remove unknown metadata or trailing blocks when possible.
## Use antivirus/ML detectors: 
trained to recognize unusual byte patterns and common polyglot constructions.
## Logging & heuristics: 
Flag uploads that contain both image and archive markers, or multiple distinct file signatures.


# Safe ways to practice / learn more

If you want hands-on experience _safely_, do it in a controlled environment (offline VM or disposable sandbox) and use benign files. Suggested resources and approaches:

- **CTF platforms** (many have challenges about polyglots/forensics): trylists like PicoCTF, HackTheBox (with safe, educational boxes), and OverTheWire.
    
- **Writeups & blog posts** — many security researchers publish analyses of benign polyglot puzzles (search for “polyglot file PNG ZIP writeup” in a safe browser).
    
- **Forensic toolkits** — practice with tools that examine file signatures and headers (read about how they work rather than using them to evade controls).
    
- **Academic papers & talks** — good for understanding detection techniques and the theory.


# More 
 + https://medium.com/%40zulfianarahmi4/my-ctf-polyglot-file-story-87eee03c1dd8
 + https://www.hoppersroppers.org/ctf/FileForensics/2-PolyglotFiles.html?utm_source=chatgpt.com
 + https://gildas-lormeau.github.io/Polyglot-HTML-ZIP-PNG/?utm_source=chatgpt.com
 + https://arxiv.org/abs/2407.01529?utm_source=chatgpt.com


# Recommended CTF Challenges / Write-ups

|Challenge / Write-up|What it is / Why it’s useful|Skills you’ll learn|
|---|---|---|
|**picoCTF “Secret of the Polyglot”**|A forensics challenge in picoCTF 2024 where you’re given a file (`flag2of2-final.pdf`) that is a polyglot — valid as both a PDF _and_ a PNG. [Medium+2InfoSec Write-ups+2](https://iritt.medium.com/picoctf-secret-of-the-polyglot-challenge-walkthrough-79dcd14340ef?utm_source=chatgpt.com)|Recognizing magic numbers, using tools like `file`, renaming extensions, extracting hidden parts, combining pieces to reconstruct flag, thinking beyond the extension.|
|**PortSwigger LAB-6: Remote Code Execution via Polyglot Web Shell Upload**|A web security/lab challenge. You bypass file type filtering by embedding malicious code inside PNG metadata, or creating a polyglot PNG/PHP file. [InfoSec Write-ups](https://infosecwriteups.com/portswigger-lab-6-remote-code-execution-via-polyglot-web-shell-upload-bug-bounty-prep-by-b426b0d50d39?utm_source=chatgpt.com)|Metadata manipulation (ExifTool etc.), understanding filtering based on content vs extension, embedding code in benign format, safe upload exploits.|
|**Neuland CTF 2022 Winter – Steganography “Trust issues”**|Has a picture that’s also a ZIP inside; ZIP is password protected. You may need to change extension and deal with some broken file headers, then brute force things. [0xffd700.com](https://0xffd700.com/neuland-ctf-2022-winter-stego?utm_source=chatgpt.com)|Working with ZIPs inside images, dealing with imperfect files (broken headers), forensics tools like `binwalk`, maybe password cracking with `john` or similar, reconstructing a corrupted or hidden file.|
|**SharkyCTF – Erwin’s File Manager**|Uploading polyglot files to extract flag parts. The write-up references a polyglot database. [CTFtime](https://ctftime.org/writeup/20567?utm_source=chatgpt.com)|Use of test polyglot files, combining flag pieces, maybe discovering server behavior regarding file type, how upload filters / file checks work.|