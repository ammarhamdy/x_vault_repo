
https://github.com/assetnote/kiterunner?tab=readme-ov-file#quick-start


---
# Converting between file formats

Kiterunner will also let you convert between the schema JSON, a kite file and a standard `txt` wordlist.

**Usage**

The format is decided by the filetype extension supplied by the `<input>` and `<output>` fields. We support `txt`, `json` and `kite`

```shell
kr kb convert wordlist.txt wordlist.kite
kr kb convert wordlist.kite wordlist.json
kr kb convert wordlist.kite wordlist.txt
```


# List and use `kr` wordlist

```sh
kr wordlist list
```

```sh
kr scan https://example.com -A apiroutes-240528
```

## Deeper use

copy the entire line of content into Kiterunner, paste it using the `kb replay` option, and include the wordlist you used:
```sh
REP="GET 401 [ 30, 1, 1] https://aqarat.codlop.sa/api/user/profile 2rFSDTIsTJ1BqNcg5alsRobuESa"

kr kb replay "$REP" -w ./wordlists/routes-large.kite
```
`kb`                      manipulate the kite-builder schema
`kb replay`      replay a kite-builder request based on the input

