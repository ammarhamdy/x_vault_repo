
https://github.com/xmendez/wfuzz

[[Supplemental Tools#Fuzzing with `Wfuzz`]]

---

`wfuzz` replaces the token `FUZZ` in the request with words from a payload (wordlist). 

You can supply payloads with `-w` (shorthand) or `-z` (full payload spec). Example:

```sh
# shorthand: -w wordlist
wfuzz -w /usr/share/wordlists/dirb/common.txt http://example.com/FUZZ

# full payload (file): -z file,<path>
wfuzz -z file,/usr/share/wordlists/dirb/common.txt http://example.com/FUZZ
```

---


