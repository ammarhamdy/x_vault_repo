

## Advantages to the `vi` editor:
- The `vi` editor is available on every Linux distribution in the world This is not true of any other editor.
- The `vi` editor can be executed both in a CLI (command line interface) and a GUI (graphical user interface).


## pronounce the `vi`:
+ The correct way to pronounce the `vi` editor is the vee-eye editor. 
+ The letters vi stand for visual, but it was never pronounced this way by the developers, but rather the letter v followed by the letter i.


## `vi` and `vim`:
+ In reality, most Linux systems don't include the original `vi`, but an improved version of it known as `vim`, for vi improved.


## `vim` modes:
+ There are three modes used in `vi`:
	+ Command mode. 
	+ Insert mode. 
	+ Ex mode.


## Command Mode Movement:
+ Initially, the program starts in command mode. 
+ Command mode is used to type commands, such as those used to move around a document, manipulate text, and access the other two modes. 
+ To return to command mode at any time, press the **Esc** key.
+ Once some text has been added into a document, to perform actions like moving the cursor, the **Esc** key needs to be pressed first to return to command mode.
+ This seems like a lot of work, but remember that `vi` works in a terminal environment where a mouse is useless.
+ Movement commands in `vi` have two aspects, a motion and an optional number prefix, which indicates how many times to repeat that motion. 
+ The general format is as follows:
```sh
[count] motion
```
+ The following table summarizes the motion keys available:

|Motion|Result|
|---|---|
|`h`|Left one character|
|`j`|Down one line|
|`k`|Up one line|
|`l`|Right one character|
|`w`|One word forward|
|`b`|One word back|
|`^`|Beginning of line|
|`$`|End of the line|


## Move cursor to specific postion:
+ These motions can be prefixed with a number to indicate how many times to perform the movement. 
+ For example, `5h` would move the cursor five characters to the left and `3w` would move the cursor three words to the right.
+ To move the cursor to a specific line number, type that line number followed by the `G` character. 
+ For example, to get to the fifth line of the file type `5G`. 
+ `1G` or `gg` can be used to go to the first line of the file, while a lone `G` will take you to the last line.
+ To find out which line the cursor is currently on, use **CTRL+G**.


## Command Mode Actions:
+ The standard convention for editing content with word processors is to use copy, cut, and paste. 
+ The `vi` program has none of these. Instead, `vi` uses the following three commands:

| Standard | Vi         | Meaning |
| -------- | ---------- | ------- |
| cut      | `d`        | delete  |
| copy     | `y`        | yank    |
| paste    | `P` \| `p` | put     |
+ the following general formats for action commands is acceptable:
```
action [count] motion
```
```
[count] action motion
```



### Delete:
+ Delete removes the indicated text from the page and saves it into the buffer, the buffer being the equivalent of the "clipboard" used in Windows or Mac OSX. 
+ The following table provides some common usage examples:

|Action|Result|
|---|---|
|`dd`|Delete current line|
|`3dd`|Delete the next three lines|
|`dw`|Delete the current word|
|`d3w`|Delete the next three words|
|`d4h`|Delete four characters to the left|


### Change:
+ Change is very similar to delete; the text is removed and saved into the buffer, ==however, the program is switched to insert mode to allow immediate changes to the text.== 
+ The following table provides some common usage examples:

| Action | Result                             |
| ------ | ---------------------------------- |
| `cc`   | Change current line                |
| `cw`   | Change current word                |
| `c3w`  | Change the next three words        |
| `c5h`  | Change five characters to the left |

### Yank:
+ Yank places content into the buffer without deleting it. 
+ The following table provides some common usage examples:

|Action|Result|
|---|---|
|`yy`|Yank current line|
|`3yy`|Yank the next three lines|
|`yw`|Yank the current word|
|`y$`|Yank to the end of the line|


### Put:
+ Put places the text saved in the buffer either before or after the cursor position.
+ Notice that these are the only two options, put does not use the motions like the previous action commands.

| Action | Result                   |
| ------ | ------------------------ |
| `p`    | Put (paste) after cursor |
| `P`    | Put before cursor        |


## Searching in vi:
+ Another standard function that word processors offer is find. 
+ Often, people use **CTRL+F** or look under the edit menu. The `vi` program uses search.
+ Search is more powerful than find because it supports both literal text patterns and regular expressions.
+ To search forward from the current position of the cursor, use the `/` to start the search, type a search term, and then press the **Enter** key to begin the search. 
+ The cursor will move to the first match that is found.
+ To proceed to the next match using the same pattern, press the `n` key. 
+ To go back to a previous match, press the `N` key.
+ If the end or the beginning of the document is reached, the search will automatically wrap around to the other side of the document.
+ To start searching backwards from the cursor position, start by typing `?`, then type the pattern to search for matches and press the **Enter** key.


## Insert Mode:
+ Insert mode is used to add text to the document.
+ There a few ways to enter insert mode from command mode, each differentiated by where the text insertion will begin. 
+ The following table covers the most common:

| Input | Purpose                                             |
| ----- | --------------------------------------------------- |
| `a`   | Enter insert mode right after the cursor            |
| `A`   | Enter insert mode at the end of the line            |
| `i`   | Enter insert mode right before the cursor           |
| `I`   | Enter insert mode at the beginning of the line      |
| `o`   | Enter insert mode on a blank line after the cursor  |
| `O`   | Enter insert mode on a blank line before the cursor |


## `ex` and `vi`:
+ Originally, the `vi` editor was called the `ex` editor. 
+ The name `vi` was the abbreviation (اختصار) of the **visual** command in the `ex` editor which switched the editor to "visual" mode.
+ In the original normal mode, the `ex` editor only allowed users to see and modify one line at a time. 
+ In the visual mode, users could see as much of the document that will fit on the screen. 
+ Since most users preferred the visual mode to the line editing mode, the `ex` program file was linked to a `vi` file, so that users could start `ex` directly in visual mode when they ran the `vi` link.
+ Eventually, the actual program file was renamed `vi` and the `ex` editor became a link that pointed the `vi` editor.


## Ex mode:
+ When the ex mode of the `vi` editor is being used, it is possible to view or change settings, as well as carry out file-related commands like opening, saving or aborting changes to a file. 
+ In order to get to the ex mode, type a `:` character in command mode.
+ The following table lists some common actions performed in ex mode:

|Input|Purpose|
|---|---|
|`:w`|Write the current file to the filesystem|
|`:w filename`|Save a copy of the current file as `filename`|
|`:w!`|Force writing to the current file|
|`:1`|Go to line number 1 or whatever number is given|
|`:e filename`|Open `filename`|
|`:q`|Quit if no changes made to file|
|`:q!`|Quit without saving changes to file|


## Overlapping between ex mode and command mode:
+ Although the ex mode offers several ways to save and quit, there's also `ZZ` that is available in command mode; this is the equivalent of `:wq`. 
+ There are many more overlapping functions between ex mode and command mode. 
+ For example, ex mode can be used to navigate to any line in the document by typing `:` followed by the line number, while the `G` can be used in command mode as previously demonstrated.

