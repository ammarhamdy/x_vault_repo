

The `vi` editor has two modes: insert and command

Type an **i** to enter the “insert” mode.
Then press the **`Esc`** key to leave insert mode.
Type `:wq` to write the file to disk and quit.
Type `:q!` + the **Enter** key to exit without save.


Control how the cursor moves, Remember that you are in command mode:

| Key | Function                                                      |
| --- | ------------------------------------------------------------- |
| `j` | Moves cursor down one line (same as down arrow)               |
| `k` | Moves cursor up line (same as up arrow)                       |
| `l` | Moves cursor to the right one character (same as right arrow) |
| `h` | Moves cursor to the left one character (same as left arrow)   |
| `w` | Moves cursor to beginning of next word                        |
| `e` | Moves cursor to end of word                                   |
| `b` | Moves cursor to beginning of previous word                    |


More `vi` cursor navigation:

|Keys|Function|
|---|---|
|`$`|Moves cursor to end of current line (same as **End** key)|
|`0` (zero)|Moves cursor beginning of current line (same as **Home** key)|
|`3G`|Jumps to third line (`nG` jumps to the nth line)|
|`1G`|Jumps to first line|
|**Shift**+**G**|Jumps to the last line|

Save and exit commands:

|Command|Function/Keys|
|---|---|
|`:x`|Will save and close the file.|
|`:wq`|Will write to file and quit.|
|`:wq!`|Will write to a read-only file, if possible, and quit.|
|`ZZ`|Will save and close. Notice that no colon `:` is used in this case.|
|`:q!`|Exit without saving changes|
|`:e!`|Discard changes and reload file|
|`:w!`|Write to read-only, if possible.|

### Move:
Move to the fourth word: `4w`


### Undo:
 `u` command for Undo the last operation
Undo the last 4 operations: `4u`


### Past:
past lasted deleted or yanked: `p`


### Copy:
Copy (or “yank”) the current word: `yw`


### Delete:
 The command `dw` (**d**elete **w**ord).
 `2dw` delete two words.
 
 Delete four characters, one at a time: `xxxx`
 Delete 14 characters: `14x` 
 Delete the five characters to the left of the cursor (type `5` then **Shift+x**): `5X`
 
 Delete the current line: `dd`
 Delete two lines, the current and the next: `2dd`

Delete from the current position to the end of the line **Shift+D**: `D` 


### Join:
Join two lines, the current and the next by typing a capital `J` (**Shift+J**): `J`


### Change to lower case or upper case:
 `~`  (**Shift+\`**) changes letter to the other case. 


### Search and delete:
Search for and delete the word `text`: 
```
:%s/text //g
```

### Insert:
Open a blank line below the current line by typing a lowercase letter `o`: `o`

Add text at the beginning of a line: `I`

`a` Moves the cursor to the right and enters insert mode.

Add text at the end of a line (uppercase `a`): `A`


## Search:
Search forward for the word `line`: type `/line`
Search for the next instance of the word `line`: press `n`
Search backward for the word `line`: type `?line`

