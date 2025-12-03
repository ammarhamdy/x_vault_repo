
`pandoc` is a powerful command-line document converter.

It can read and write a huge range of markup and document formats, making it useful for tasks like converting Markdown to `PDF`, Word to `HTML`, `LaTeX` to `DOCX`, and much more.


* * *

# What `Pandoc` Does

`Pandoc` converts documents _between formats_. Examples:
* Markdown → PDF    
* Word (`.docx`) → Markdown
* Markdown → `HTML`
* `HTML` → `EPUB`
* `LaTeX` → Word
* And dozens more

* * *

# Basic Syntax
```bash
pandoc inputfile -o outputfile
```
Pandoc determines formats automatically from file extensions (e.g., `.md`, `.docx`, `.pdf`).


---

# Common Options

**Specify input/output formats**
```bash
pandoc -f markdown -t html input.md -o output.html
```

 **Convert Markdown → PDF**  (Requires `LaTeX` installed)
```bash
pandoc file.md -o file.pdf
```

**Add a table of contents**
```bash
pandoc file.md -o file.pdf --toc
```

**Apply a template**
```bash
pandoc input.md -o output.html --template=template.html
```

**Include metadata**
```bash
pandoc input.md -o output.pdf \
  -V author="Alice" -V title="My Document"
```
