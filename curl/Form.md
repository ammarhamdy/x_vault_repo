


```sh
  curl 'https://manahel.codlop.sa/dashboard/blogs' \
    -H 'accept: application/json, text/javascript, */*; q=0.01' \
    -H 'accept-language: en-US,en;q=0.9' \
    -H 'origin: https://manahel.codlop.sa' \
    -H 'priority: u=1, i' \
    -H 'referer: https://manahel.codlop.sa/dashboard/blogs/create' \
    -H 'sec-ch-ua: "Chromium";v="140", "Not=A?Brand";v="24", "Google Chrome";v="140"' \
    -H 'sec-ch-ua-mobile: ?0' \
    -H 'sec-ch-ua-platform: "Linux"' \
    -H 'sec-fetch-dest: empty' \
    -H 'sec-fetch-mode: cors' \
    -H 'sec-fetch-site: same-origin' \
    -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36' \
    -H "x-csrf-token: ${token}" \
    -H 'x-requested-with: XMLHttpRequest' \
    -b "remember_admin_59ba36addc2b2f9401580f014c7f58ea4e30989d=${admin_token}; manahil_web_session=${manahil_web_session}; XSRF-TOKEN=${xsrf_token}; laravel_session=${laravel_session}; manahil_admin_session=${manahil_admin_session}" \
    -F "_token=${token}" \
    -F 'title=blog-title' \
    -F "publisher_name=publisher-name" \
    -F "image=@dark_gray.png" \
    -F "show_in_slider=0" \
    --form-string "content=<p>${my_content}</p>" \
    --form-string "notes=<p>${my_notes}</p>"
```

```
-F "content=<p>content - data<p>"
```
Why it fails
When you use `-F "content=<something>"`, curl interprets `<file>` syntax.

Example:
+ `-F "file=@/path/file.png"` → upload a file.
+ `-F "file=<data.txt"` → upload the contents of `data.txt`.

So your `<p>`content - data`<p>` makes curl look for a file named `p>content - data<p`, which doesn’t exist → boom 💥.


