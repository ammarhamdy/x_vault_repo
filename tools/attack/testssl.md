

https://testssl.sh/
https://www.kali.org/tools/testssl.sh/

---

`testssl.sh` is a command-line tool for testing SSL/TLS security on a server. It checks which protocols, ciphers, and vulnerabilities a server supports.

# installation
```sh
sudo apt install testssl.sh
```

# Run it against a hostname (or IP):
```sh
testssl example.com
```

# Specify a Port
```sh
testssl example.com:8443
```

# Fast scan (protocols + vulnerabilities):
```sh
testssl -U --fast example.com
```

# Check only protocols:
```sh
testssl -p example.com
```

# Check only vulnerabilities:
```sh
testssl -V example.com
```

# Check ciphers:
```sh
testssl -e example.com
```

# Output Options

## Save results in JSON:
```sh
testssl -oJ results.json example.com
```

## Save in HTML:
```sh
testssl -oH results.html example.com
```