Ubuntu includes built-in utilities to compute SHA‑2 hashes. 

SHA‑2 is a family of hash functions including SHA‑224, SHA‑256, SHA‑384, and SHA‑512. 


```sh
sha256sum filename.txt
sha512sum filename.txt
echo -n "your string here" | sha256sum
```

Using `OpenSSL`:
```sh
openssl dgst -sha256 filename.txt
echo -n "your string here" | openssl dgst -sha256
```




