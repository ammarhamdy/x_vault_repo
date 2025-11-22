
https://www.kali.org/tools/dirsearch/

----

An advanced command-line tool designed to brute force directories and files in webservers

---
# Installation 

## Using `apt`
```sh
sudo apt install dirsearch
```

## From `githup` 

```
git clone https://github.com/maurosoria/dirsearch.git
```

**Make it globally accessible**
```sh
sudo ln -s $(pwd)/dirsearch.py /usr/local/bin/dirsearch
```


# Run
```sh
dirsearch -u https://example.com
```


# Wordlists

Default wordlists (already included)

When you clone `dirsearch`, it already comes with its own wordlists inside the `db/` folder:
```sh
dirsearch/db/dicc.txt
```

## SecLists (very popular)
[SecLists](https://github.com/danielmiessler/SecLists?utm_source=chatgpt.com) is a massive collection of wordlists for **directories, files, usernames, passwords, fuzzing, and more**.
```sh
git clone https://github.com/danielmiessler/SecLists.git
```
- `SecLists/Discovery/Web-Content/common.txt` → basic directory brute-forcing
- `SecLists/Discovery/Web-Content/big.txt` → larger, more thorough scan
- `SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt` → from DirBuster, very popular


## Example usage with SecLists

```sh
python3 dirsearch.py -u https://example.com -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

```sh
python3 dirsearch.py -u https://example.com -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt -e php,html,js,txt
```
**`-e php,html,js,txt`** 
This tells `dirsearch` to **append these extensions** to each word in the wordlist when making requests.

