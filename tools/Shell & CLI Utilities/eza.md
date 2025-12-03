
`eza` is a modern, user-friendly replacement for the classic `ls` command on Linux and other Unix-like systems.

---

# Installation
```sh
sudo apt install eza
```

# Basic file listing (like `ls`)
```bash
eza
```

# Long format (like `ls -l`)

```bash
eza -l
```

```sh
eza -l --sort=size
```

# Show hidden files
```bash
eza -a
```

# Human-readable sizes
```bash
eza -lh
```

# Recursive directory tree

```bash
eza -T
```

```sh
eza -T --level=2
```

# Show Git status for files
```bash
eza --git
```

