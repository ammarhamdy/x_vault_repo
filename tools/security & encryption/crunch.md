# Enumerations

$$
base^n
$$

## Letters
- **5 characters**
- Each can be from **a–z** (26 choices per character).
$$26^5$$
```less
11,881,376 possible passwords
```

## Letters and numbers
- **5 characters**, each with **26 choices** (letters).
- **2 characters**, each with **10 choices** (digits).
$$
26^5*10^2 
$$
```less
1,188,137,600 possible passwords
```


# Special character
On a **standard US QWERTY keyboard** 

## 10 Digits row (using Shift key):
```
! @ # $ % ^ & * ( )
```

## 20 Punctuation keys
```
- _ = + [ { ] } \ | ; : ' " , < . > / ?
```

## 2 Grave/tilde key
```
` ~
```



---
# Create Custom Word-lists Using Crunch in Kali Linux

https://www.linuxfordevices.com/tutorials/kali-linux/create-custom-wordlists-using-crunch

https://medium.com/@techdefenderhub/how-to-create-custom-password-wordlists-with-crunch-da8a43a1195e

https://www.hackingarticles.in/crunch-wordlist-generation-guide/

```
crunch <min> <max> <charset> <options>
```

- min: It is the minimum password length
- max: It is the maximum password length
- charset: Character set to be used
- options: options to be used (like -o to save the output to a file)

To save the output to a file, use -o by running the following command:

```sh
crunch 3 6 0123456789 -o list.txt
```

If you want to create a word-list with passwords of 10 character that ends with 123, You can do so by executing the following command:

```sh
crunch 10 10 @@@@@@@123 -o list1.txt
```


# Wildcard Characters in Crunch

| Wildcard | Meaning                           |
| -------- | --------------------------------- |
| `%`      | Any **digit** (0-9)               |
| `@`      | Any **lowercase letter** (a-z)    |
| `,`      | Any **uppercase letter** (A-Z)    |
| `^`      | Any **symbol** (e.g., `!@#$%^&*`) |


# Generate 5-Digit Enumerations
```sh
crunch 5 5 -t %%%%% -o output.txt
```
- `5 5`: Specifies the minimum and maximum length of generated strings (5 characters).
- `-t %%%%%`: Uses `%` as a wildcard, which represents numeric digits (`0-9`).
- `-o output.txt`: Saves the output to `output.txt` (optional).


# Using Fixed Characters
```sh
crunch 8 8 -t Pass%%%%
```
➡ Output: `Pass0000`, `Pass0001`, ..., `Pass9999`


# Generate custom pattern passwords (e.g, "ABCD12")
```sh
crunch 6 6 -t ABCD%%
```
➡ Output: `ABCD00`, `ABCD01`, ..., `ABCD99`


# Generate strong passwords with symbols
```sh
crunch 8 8 -t @@%%^^!!
```
➡ Output: `aa00!!@@`, `aa00!!@#`, ..., `zz99##$$`


# See man page example 11 
```sh
>> crunch 3 3 abc + 123 -t @%-

Crunch will now generate the following number of lines: 9 
a1-
a2-
a3-
b1-
b2-
b3-
c1-
c2-
c3-
```


---

# Real live example
	
```sh
crunch 15 15 -t abdullmajeed^% -o post.txt
```

```sh
abdullmajeed!0
abdullmajeed!1
abdullmajeed!2
abdullmajeed!3
abdullmajeed!4
...
abdullmajeed 5
abdullmajeed 6
abdullmajeed 7
abdullmajeed 8
abdullmajeed 9
```


