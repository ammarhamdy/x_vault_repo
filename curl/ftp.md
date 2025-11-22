
# general syntax
You can use `curl` with the `ftp://` protocol to download files from 
an FTP server.
```sh
curl -u username:password ftp://ftp.server.com/path/to/file -o localfile
```

Some servers may require **FTPS (FTP over SSL/TLS)** instead of plain FTP; in that case, you’d use `--ftp-ssl` or `--ssl`.

---


# Anonymous FTP download
```sh
curl ftp://ftp.server.com/pub/example.txt -o example.txt
```

# Download multiple files using a wildcard (if the server supports it):
```sh
curl -u myuser:mypassword "ftp://ftp.server.com/pub/*.txt" -O
```

# Verbose mode (helpful for debugging):
```sh
curl -v -u myuser:mypassword ftp://ftp.server.com/pub/example.txt -O
```



