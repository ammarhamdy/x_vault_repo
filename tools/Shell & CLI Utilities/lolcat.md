
https://github.com/busyloop/lolcat

---

lolcat is a command-line utility for Unix-like operating systems, including Linux, BSD, and macOS, designed to display text output in vibrant rainbow colors. It functions similarly to the cat command, but with the added effect of colorizing the text. 

---
# Installation
```sh
sudo apt  install lolcat
```

# Colorizing text from a file
```sh
lolcat my_file.txt
```

# Colorizing the output of another command

```sh
ls -l | lolcat
```

# Creating a colorful banner with [[figlet]]
```sh
figlet "Hello World" | lolcat
```

# Animating the colors
```sh
ls -l | lolcat -a -d 100
```
`-a` flag enables animation 
`-d` sets the duration in milliseconds.

# Keep single color (almost no gradient)
```sh
echo "Hello, world!" | lolcat -F 0
```
`-F 0` fixes the frequency, so it’s not shifting colors.

# Make colors more spread out (bigger blocks)
```sh
echo "Hello, world!" | lolcat -p 1000
```

