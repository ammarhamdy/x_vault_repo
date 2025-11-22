
website:
https://curl.se/

doc:
https://everything.curl.dev/index.html

man page:
https://curl.se/docs/manpage.html


---
The curl command is used to transfer data from or to a server using various protocols such as HTTP, HTTPS, FTP, SCP, SFTP, and more. The basic syntax is:

```sh
curl [options] [URL...]
```

To retrieve a web page and display its content in the terminal, simply run:

```sh
curl http://example.com
```
**weather request**
```sh
curl https://wttr.in/egypt
```


`-o` or `--output` specifies the output file name. 
For example, to download a file and save it as "`myfile.txt`":
```sh
curl -o myfile.txt http://example.com/file.txt
```

----

# Show only status code
```sh
curl -s -o /dev/null -w "%{http_code}\n" https://example.com
```
`-w "%{http_code}\n"` (Write Output Format)
`-s` (Silent Mode)
`-o /dev/null` (Discard Output)


Use Curl to Check HTTP/3 Support
```sh
curl -I --http3 https://www.cloudflare.com
```

---

# Typical combined effect
- follows redirects,
- requests compressed responses and decompresses them,
- stays silent on success (no progress meter),
- prints helpful error messages on failure,
- treats HTTP 4xx/5xx as errors (no body printed),
- and never runs longer than 30 seconds.
```sh
if curl -sS -L --fail --compressed --max-time 30 "https://example.com/api" -o response.json; then
  echo "OK — response saved to response.json"
else
  echo "Request failed" >&2
  exit 1
fi
```

`-sS`
- `-s` = **silent**. Suppresses the progress meter and non-error messages.
- `-S` = **show error**. When used together as `-sS`, curl stays quiet _except_ it will still print error messages. This is a common pattern for scripts: hide normal progress, but show errors.

`-L`
- **Follow redirects.** If the server responds with a `3xx` redirect (Location header), curl will follow it automatically to the final URL. (==By default curl follows up to 50 redirects==.)

`--fail` (a.k.a `-f`)
- **Exit on HTTP errors.** Causes curl to return a non-zero exit status and not output the response body when the HTTP status is 400 or higher. Useful in scripts so you can detect failed requests by checking the exit code.
- Note: With `-L`, `--fail` applies to the **final** response after following redirects.

`--show-error`
- Equivalent to `-S`. If you used `-s` to silence curl, `--show-error` makes sure curl still prints error messages to `stderr`. Useful to combine with `-s` so scripts remain quiet on success but informative on failure.

`--compressed`
- Request a compressed response from the server by sending `Accept-Encoding` (`gzip`/deflate) and automatically **decompress** the response body for you. Saves bandwidth and is transparent to your script (curl handles decompression). Requires `libcurl` built with `zlib` support.

`--max-time 30`
- **Total timeout** (in seconds) for the entire operation. If the whole request (connect + transfer + redirects) takes longer than 30 seconds, curl cancels the request and returns an error. Handy to avoid hangs in scripts.
- For finer control you can also use `--connect-timeout <seconds>` to limit only the connection phase.

---
# Examples


```bash
curl --path-as-is -i -s -k -X 'GET' \
    -H 'Host: elkadih.codlop.sa' \
    -H 'Sec-Ch-Ua: "Chromium";v="131", "Not_A Brand";v="24"' \
    -H 'Sec-Ch-Ua-Mobile: ?0' \
    -H 'Sec-Ch-Ua-Platform: "Linux"' \
    -H 'Accept-Language: en-US,en;q=0.9' \
    -H 'Upgrade-Insecure-Requests: 1' \
    -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.140 Safari/537.36' \
    -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7' \
    -H 'Sec-Fetch-Site: none' \
    -H 'Sec-Fetch-Mode: navigate' \
    -H 'Sec-Fetch-User: ?1' \
    -H 'Sec-Fetch-Dest: document' \
    -H 'Accept-Encoding: gzip, deflate, br' \
    -H 'Priority: u=0, i' \
    'https://elkadih.codlop.sa/'
```
- **`--path-as-is`** → Prevents `curl` from normalizing or modifying the URL path.
- **`-i`** → Includes the response **headers** in the output.
- **`-s`** → Runs in **silent mode** (hides progress bar/errors).
- **`-k`** → Ignores SSL/TLS certificate verification (useful for self-signed certificates).
- **`-X 'GET'`** → Specifies the HTTP method as `GET`.
+ `-H 'Host: elkadih.codlop.sa'` -> Host header


![[Pasted image 20250203140741.png]]
```sh
curl --path-as-is -i -s -k -X 'PATCH' \
    -H 'Host: 0ace00ce0349ea95803cee9b000b006a.web-security-academy.net' \
    -H 'Sec-Ch-Ua-Platform: "Linux"' \
    -H 'Accept-Language: en-US,en;q=0.9' \
    -H 'Sec-Ch-Ua: "Chromium";v="131", "Not_A Brand";v="24"' \
    -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.140 Safari/537.36' \
    -H 'Sec-Ch-Ua-Mobile: ?0' \
    -H 'Accept: */*' \
    -H 'Sec-Fetch-Site: same-origin' \
    -H 'Content-Type: application/json;' \
    -H 'Sec-Fetch-Mode: cors' \
    -H 'Sec-Fetch-Dest: empty' \
    -H 'Referer: https://0ace00ce0349ea95803cee9b000b006a.web-security-academy.net/product?productId=3' \
    -H 'Accept-Encoding: gzip, deflate, br' \
    -H 'Priority: u=1, i' \
    -H 'Content-Length: 15' \
    -b 'session=W9e7CI8Kg5Dt5kL5FzsxZaZgYHfqUDtS' \
    --data-binary '{\r\n"price":0\r\n}' \
    'https://0ace00ce0349ea95803cee9b000b006a.web-security-academy.net/api/products/3/price'

```


