
[colors](https://upload.wikimedia.org/wikipedia/commons/1/15/Xterm_256color_chart.svg)

# Prompt String

To modify the terminal prompt, you’ll need to edit the `PS1` variable in your shell configuration file

On most Linux systems, the default `PS1` variable looks like this:
```
\u@\h:\w$\$
```
- `\u`: username
- `@`: at symbol
- `\h`: hostname (computer name)
- `:`: colon
- `\w`: current working directory (with `$HOME` abbreviated as ~)
- `\$`: dollar sign (normal user) or `#` (root user)

**Colorize the prompt**: 
```
PS1="\[\033[1;32m\]\u@\h:\w$\[\033[0m\]"` (green color)
```



My PS1
```
$ echo $PS1
\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$

```

- Use `\d` to display the date in the format `YYYY-MM-DD`.
- Use `\w` to display the current working directory (with `$HOME` abbreviated as ~).
- Use `\W` to display the basename of the current working directory (without `$HOME` abbreviation).
- Use `\\[` and `\\]` to embed non-printing characters, such as terminal control sequences.
- - **`\a`** – A bell character
- **`\D{format}`** – Use this to call the system to respond with the current time
- **`\e`** – Escape character
- **`\h`** – Hostname (short)
- **`\H`** – Full hostname (domain name)
- **`\j`** – Number of jobs being managed by the shell
- **`\l`** – The basename of the shells terminal device
- **`\n`** – New line
- **`\r`** – Carriage return
- **`\s`** – The name of the shell
- **`\t`** – Time (hour:minute:second)
- **`\@`** – Time, 12-hour AM/PM
- **`\A`** – Time, 24-hour, without seconds
- **`\u`** – Current username
- **`\v`** – BASH version
- **`\V`** – Extra information about the BASH version
- **`\!`** – Lists this command’s number in the history
- **`\#`** – This command’s command number
- **`\$`** – Specifies whether the user is root (#) or otherwise (\$)
- **\\**– Backslash
- **`\[`** – Start a sequence of non-displayed characters (useful if you want to add a command or instruction set to the prompt)
- **`\]`** – Close or end a sequence of non-displayed characters


**Saving Changes**
After modifying the `PS1` variable, you’ll need to save the changes to your shell configuration file.
The location of this file varies depending on your Linux distribution:
- Ubuntu/Debian: `~/.bashrc`



-----
## ANSI escape sequences

ANSI escape sequences are a standard for controlling text formatting, colors, and cursor movement on text-based terminals. 

They are widely used in command-line interfaces (CLI), terminal emulators, and applications that run in text mode.

These sequences begin with the **escape character** (ASCII code 27, or `\033`), followed by a series of codes to define how the text should be formatted or where the cursor should move.

### Basic Structure

The typical structure of an ANSI escape sequence is as follows:

```
\033[<code1>;<code2>;...m
```

- `\033` (or `\e`) represents the **escape character**.

- The `[` character starts the **control sequence**.

- `<code1>;<code2>;...` are the **parameter codes** (a series of numeric values) that specify the behavior, such as changing text color, style, or cursor position.

- `m` is a common letter for formatting (but other letters, such as `A`, `B`, `C`, etc., can be used for cursor movement or other actions).

### Common ANSI Escape Sequences

#### Text Formatting

These are used to change the style of text, such as making it bold, underlined, or resetting the formatting.

|Code|Effect|
|---|---|
|0|Reset / Normal|
|1|Bold|
|4|Underlined|
|5|Blink|
|7|Inverse (swap foreground and background colors)|
|22|Normal intensity (un-bold)|
|24|Remove underline|
|25|Remove blink|

#### Text Color

You can change the foreground (text) and background colors using ANSI codes.

- **Foreground Colors**: `\033[3Xm` (X = color code)
- **Background Colors**: `\033[4Xm` (X = color code)

| X   | Color   |
| --- | ------- |
| 0   | Black   |
| 1   | Red     |
| 2   | Green   |
| 3   | Yellow  |
| 4   | Blue    |
| 5   | Magenta |
| 6   | Cyan    |
| 7   | White   |

For example:
- **Red Text**: `\033[31m`
- **Green Background**: `\033[42m`
- **Reset**: `\033[0m`

#### Cursor Movement

ANSI escape sequences can also control cursor position and screen manipulation:

|Sequence|Effect|
|---|---|
|`\033[A`|Move cursor up one line|
|`\033[B`|Move cursor down one line|
|`\033[C`|Move cursor right one character|
|`\033[D`|Move cursor left one character|
|`\033[n;mH`|Move cursor to row `n`, column `m`|
|`\033[2J`|Clear the screen|
|`\033[K`|Clear from cursor to end of line|

For example:
- Move the cursor to the **5th row, 10th column**:  
    `\033[5;10H`
- Clear the screen:  
    `\033[2J`

### Extended Colors

For more than the basic 8 colors, you can use **256-color mode**:

- **Foreground**: `\033[38;5;<n>m`
- **Background**: `\033[48;5;<n>m`

Where `<n>` is a number from 0 to 255.

### Example Usage in a Bash Script
```
#!/bin/bash

# Define some colors
RED='\033[31m'
GREEN='\033[32m'
RESET='\033[0m'

echo -e "${RED}This is red text${RESET}"
echo -e "${GREEN}This is green text${RESET}"
```


```
PS1="\033[40;32m\]\t\033[00m\] \033[34m\w\033[00m\]\n\$"
```

```
PS1="\033[42;30m\][\033[00m\]\033[40;32m\]\t\033[00m\]\033[42;30m\]]\033[00m\] \033[34m\w\033[00m\]\n_\$"
```


```
PS1="\033[30m\][\033[00m\]\033[32m\]\t\033[00m\]\033[30m\]]\033[00m\] \033[34m\w\033[00m\]\n_\$"
```

---
# REplains why `\[` and `\]` are necessary.

see:
https://askubuntu.com/questions/404341/where-can-i-find-a-complete-reference-for-the-ps1-variable

https://tldp.org/HOWTO/Bash-Prompt-HOWTO/nonprintingchars.html


```
PS1='\[\033[1;33m\]>\[\033[0m\] '
```

---
# `bashrc`

where config file live:
```
nano ~/.bashrc
```

Reset
```
cp /etc/skel/.bashrc ~/
source ~/.bashrc
```

---
# Examples


```
┌──(kali㉿kali)-[~]
└─$ echo $PS1
%F{%(#.blue.green)}┌──${debian_chroot:+($debian_chroot)─}${VIRTUAL_ENV:+($(basename $VIRTUAL_ENV))─}(%B%F{%(#.red.blue)}%n㉿%m%b%F{%(#.blue.green)})-[%B%F{reset}%(6~.%-1~/…/%4~.%5~)%b%F{%(#.blue.green)}]
└─%B%(#.%F{red}#.%F{blue}$)%b%F{reset} 

```


```
PS1="┌──[\033[32m\]\t\033[00m\]] \033[34m\w\033[00m\]\n└─\$"
```

```
PS1="┌──⸢\033[34m\w\033[00m\]⸥\n└─〉"
```

```
PS1="\033[35m\]⸢\033[0m\]\033[34m\]\w\033[0m\]\033[35m\]⸥\033[0m\]"
```