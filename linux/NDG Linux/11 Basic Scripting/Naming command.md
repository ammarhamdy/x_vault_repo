
# Keep It Short, But Descriptive

Aim for a **single word** (like `grep`, `curl`, `htop`) or a **short compound** (`git-clone`, `kubectl`).

**Bad:** `extract-data-from-csv-with-filtering`  
**Good:** `csvfilter`


# Lowercase Only

Command names should be **all lowercase**.


# No Spaces or Special Characters

Use **hyphens** if needed, not underscores or spaces.
Avoid symbols like `!`, `@`, `$`, etc.

**Good:** `my-tool`, `log-analyzer`  
**Avoid:** `my_tool`, `log analyzer`


# Optional: Use Verb-Noun Style

Especially if it's a CLI suite, this improves clarity:
```
task-add
user-create
log-analyze
```


# Use a `--help` Flag

Even though this is not about the name, it's part of good CLI design.


# Example of a Well-Named CLI Tool

Let's say you're making a CLI for managing notes:
- Good name: `noted`
    - Short, unique, memorable.
    - Could offer sub-commands like:
```sh
noted new
noted list
noted remove 2
```

