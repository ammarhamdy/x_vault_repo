
Examples: https://gist.github.com/LunaCodeGirl/6707775

----

`FIGlet` is a command-line utility for Linux and other operating systems that generates large text banners, or "ASCII art," from ordinary text input. It transforms plain text into visually striking designs using various specialized font files composed of smaller ASCII characters.

**Key Features**:

**ASCII Art Generation**:
Converts standard text into large, stylized characters made from ASCII symbols.

**Font Variety**:
Utilizes a wide range of `.flf` font files, each offering a distinct artistic style for the generated text.

**Customization**:
Allows users to control aspects like justification (left, right, center), output width, and "smashing" rules, which dictate how adjacent characters are merged or compressed

**Versatility**:
Commonly used for decorative purposes in shell scripts, `motd` (message of the day) files, `READMEs`, and text-based presentations. 


----

# Installation
```sh
sudo apt install figlet
```

# Basic Usage

To use figlet, simply type figlet followed by the text you want to convert:
```sh
figlet Hello World
```

**Using Different Fonts**:
You can specify a particular font using the -f option:
```
figlet -f slant "Linux Fun"
```

To see a list of available fonts, you can use the `showfigfonts` command.