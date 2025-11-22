
## Ways of injecting OS commands

You can use a number of shell metacharacters to perform OS command injection attacks.
A number of characters function as command separators, allowing commands to be chained together. 
The following command separators work on both Windows and Unix-based systems:
- `&` (Background Execution)
- `&&` (Logical AND)
- `|` (Pipe Operator)
- `||` (Logical OR)


The following command separators work only on Unix-based systems:
- `;`
- Newline (`0x0a` or `\n`)


On Unix-based systems, you can also use backticks or the dollar character to perform inline execution of an injected command within the original command:
- `` ` ``injected command `` ` ``
- `$(`injected command `)`


