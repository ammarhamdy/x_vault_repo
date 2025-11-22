
**URL encoding** (also known as percent-encoding) is a way to encode information in a Uniform Resource Locator (URL). 

It is used to encode special characters that might otherwise have a different meaning in URLs or are not allowed in certain parts of a URL.

URL encoding (or percent‐encoding) represents any 8‑bit byte as a "%" followed by two hexadecimal digits.

In other words, every possible byte value (from 0 to 255) can be expressed in URL encoding.

There are 256 possible combinations—from **%00** through **%FF**.

URL encoding is defined in various RFCs (such as RFC 3986) and widely documented on developer resources like MDN and Wikipedia
[developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)
[en.wikipedia.org](https://en.wikipedia.org/wiki/Percent-encoding)


# How it works
- Certain characters in a URL have a special meaning, such as `:` for separating the scheme, `/` for path separation, `?` for query parameters, and `#` for fragments.
- Unsafe characters are replaced with a `%` followed by their ASCII hexadecimal value.
- Spaces, for example, are encoded as `%20` or `+` (in query strings).


# Common Encodings

| Name          | Character | URL Encoding | ASCII Hex |
| ------------- | --------- | ------------ | --------- |
| Space         |           | %20          | 0x20      |
| Exclamation   | !         | %21          | 0x21      |
| Quote         | "         | %22          | 0x22      |
| Hash          | #         | %23          | 0x23      |
| Dollar        | $         | %24          | 0x24      |
| Percent       | %         | %25          | 0x25      |
| Ampersand     | &         | %26          | 0x26      |
| Apostrophe    | '         | %27          | 0x27      |
| Left Paren    | (         | %28          | 0x28      |
| Right Paren   | )         | %29          | 0x29      |
| Asterisk      | *         | %2A          | 0x2A      |
| Plus          | +         | %2B          | 0x2B      |
| Comma         | ,         | %2C          | 0x2C      |
| Minus         | -         | %2D          | 0x2D      |
| Period        | .         | %2E          | 0x2E      |
| Slash         | /         | %2F          | 0x2F      |
| Colon         | :         | %3A          | 0x3A      |
| Semicolon     | ;         | %3B          | 0x3B      |
| Less Than     | <         | %3C          | 0x3C      |
| Equals        | =         | %3D          | 0x3D      |
| Greater Than  | >         | %3E          | 0x3E      |
| Question      | ?         | %3F          | 0x3F      |
| At            | @         | %40          | 0x40      |
| Left Bracket  | [         | %5B          | 0x5B      |
| Backslash     | \         | %5C          | 0x5C      |
| Right Bracket | ]         | %5D          | 0x5D      |
| Caret         | ^         | %5E          | 0x5E      |
| Underscore    | _         | %5F          | 0x5F      |
| Backtick      | `         | %60          | 0x60      |
| Left Brace    | {         | %7B          | 0x7B      |
| Vertical Bar  | \|        | %7C          | 0x7C      |
| Right Brace   | }         | %7D          | 0x7D      |
| Tilde         | ~         | %7E          | 0x7E      |


# Characters that need encoding

1. Reserved characters (with special meaning in URLs):  
    `: / ? # [ ] @ ! $ & ' ( ) * + , ; =`
2. Unsafe characters:  
    Non-printable characters, spaces, and certain symbols.

## Reserved characters in URLs

When we talk about **“reserved” characters in URLs**, it comes from the official standard **RFC 3986 (Uniform Resource Identifier: Generic Syntax)**.

These characters have **special meanings** in URLs and cannot always be used literally — if you want them as data, they must be **percent-encoded**.

### Reserved characters (per RFC 3986)
They’re split into two groups:
- **General delimiters** (used to structure the URL itself):
    `:  /  ?  #  [  ]  @`
- **Sub-delimiters** (often used in query strings, path segments, etc.):
    `!  $  &  '  (  )  *  +  ,  ;  =`
### Unreserved characters
These **do not need encoding** because they’re safe anywhere in a URL:
`A–Z  a–z  0–9  -  .  _  ~`

### Everything else
All other ASCII characters (spaces, quotes, `<`, `>`, `{`, `}`, etc.) are neither reserved nor unreserved, and **must always be percent-encoded** if used in URLs.


# Encoding a Full URL
**Original URL:** 
`https://example.com/search?query=hello world&filter=new`
**Encoded URL:**  
`https://example.com/search?query=hello%20world&filter=new`


# Practical Use

In programming, libraries and functions can handle URL encoding/decoding:

```python
from urllib.parse import quote, unquote

quote("Hello World!")  # "Hello%20World%21"
unquote("Hello%20World%21")  # "Hello World!"

```

Query parameters are appended to the end of the request URL, following `?` and listed in key-value pairs, separated by `&` as follows: `?id=1&type=new`

Path parameters form part of the request URL, and are referenced using placeholders preceded by `:` as in the following example: `/customer/:id`

The processor will encode characters depending on where they occur in the URL:

| URL component | Characters to encode                                                       |
| ------------- | -------------------------------------------------------------------------- |
| Path          | `"` `<` `>` `` ` `` `#` `?` `{` `}` `SPACE`                                |
| Query         | `"` `#` `&` `'` `<` `=` `>` `SPACE`                                        |
| Userinfo      | `"` `<` `>` `` ` `` `#` `?` `{` `}` `/` `:` `;` `=` `@`<br>`[` `\` `]` `^` |


# Encode text into url encoding 

**handy one-liner URL encoder**.
```sh
echo "hello world & foo=bar" | jq -sRr @uri 
# hello%20world%20%26%20foo%3Dbar
```

