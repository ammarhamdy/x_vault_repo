
The `less` command in Ubuntu (and most Unix-like systems) is a **pager** — it lets you view (but not edit) text files one screen at a time. 

It’s much more powerful than `cat` or `more`, especially for searching and navigating large files like logs or configuration files.

---

# Searching in `less`

|Command|Action|
|---|---|
|`/pattern`|Search **forward** for “pattern”|
|`?pattern`|Search **backward** for “pattern”|
|`n`|Repeat last search in the **same direction**|
|`N`|Repeat last search in the **opposite direction**|
|`&pattern`|Show only lines that **match** “pattern” (like a live filter)|

## Example Search Flow
- Type `/error` → press **Enter**  → jumps to the first occurrence of “error”
- Press `n` to go to the next “error”
- Press `N` to go to the previous “error”
- To filter only lines containing “error”: Type `&error`

# Common Navigation Keys
|Key|Action|
|---|---|
|↑ / ↓|Move one line up/down|
|Spacebar|Move one page forward|
|`b`|Move one page backward|
|`g`|Go to the beginning of the file|
|`G`|Go to the end of the file|
|`q`|Quit `less`|

Case-insensitive search: use `/pattern` and add `-i` flag.