

```sh
printf FORMAT [ARGUMENT1] [ARGUMENT2] ...
```
`FORMAT`: A string that specifies how the arguments should be formatted.


**Format Specifiers:**
- Format specifiers start with a `%` character and end with a conversion character.
+ Between the `%` and the conversion character, you can include optional flags, field widths, and precision specifiers.


**Common Conversion Characters:**
- `%s`: String.
- `%d` or `%i`: Signed decimal integer.
- `%u`: Unsigned decimal integer.
- `%f` or `%F`: Floating-point number.
- `%x` or `%X`: Hexadecimal integer.
- `%o`: Octal integer.
- `%c`: Character.
- `%%`: Prints a literal `%` character.


**Flags:**
- `-`: Left-align the output within the field.
- `0`: Pad the output with zeros.
- `+`: Always include a sign (`+` or `-`) for numeric values.
- (space): Precede positive numbers with a space.
- `#`: Use an alternate form for the conversion (e.g., `0x` for hexadecimal).


**Examples:**

**Printing a string with left-padding:**
```sh
printf "% 10s\n" "hello"
```

**Printing an integer with zero-padding:**
```sh
printf "%05d\n" 123 # 00123
```

**Printing a floating-point number with precision:**
```sh
printf "%.2f\n" 3.14159 # 3.14
```

**Printing multiple arguments:**
```sh
printf "%-10s %5d %.2f\n" "Name" 25 3.14 # Name 25 3.14
```

**Print repeated character:**
```sh
printf "%0.s-" {1..10}
```
`"%0.s-"`: The format string.
- `%0.s`: This part is a bit of a trick. The `%s` format specifier expects a string, and `%0.s` effectively tells `printf` to print an empty string for each argument.
- `-`: This is the character you want to repeat.