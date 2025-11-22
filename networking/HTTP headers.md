## Secure Client Hints `Sec-Ch`

**Client Hints Headers (`Sec-Ch-*`)**
```sh
curl -X GET https://example.com \
    -H "Sec-Ch-Ua: \"Chromium\";v=\"131\", \"Not_A Brand\";v=\"24\"" \
    -H "Sec-Ch-Ua-Arch: \"x86\"" \
    -H "Sec-Ch-Ua-Bitness: \"64\"" \
    -H "Sec-Ch-Ua-Full-Version: \"131.0.6778.140\"" \
    -H "Sec-Ch-Ua-Full-Version-List: \"Chromium\";v=\"131\", \"Not_A Brand\";v=\"24\"" \
    -H "Sec-Ch-Ua-Mobile: ?0" \
    -H "Sec-Ch-Ua-Model: \"Pixel 7\"" \
    -H "Sec-Ch-Ua-Platform: \"Linux\"" \
    -H "Sec-Ch-Ua-Platform-Version: \"10.0\"" \
    -H "Sec-Ch-Prefers-Reduced-Motion: ?1" \
    -H "Sec-Ch-Prefers-Color-Scheme: \"dark\""

```
`Sec-Ch-Ua`	Provides information about the user agent (browser type and version).
`Sec-Ch-Ua-Arch`	Specifies the architecture of the device (e.g., "x86", "arm").
`Sec-Ch-Ua-Bitness`	Indicates the bitness of the OS (e.g., "64").
`Sec-Ch-Ua-Full-Version`	Full version of the browser (e.g., "131.0.6778.140").
`Sec-Ch-Ua-Full-Version-List`	Lists full versions of compatible browsers.
`Sec-Ch-Ua-Mobile`	Indicates if the device is mobile (?0 = false, ?1 = true).
`Sec-Ch-Ua-Model`	Provides the device model name (e.g., "Pixel 7").
`Sec-Ch-Ua-Platform`	Specifies the operating system (e.g., "Windows", "Linux", "Android").
`Sec-Ch-Ua-Platform-Version`	Specifies the version of the OS (e.g., "10.0").
`Sec-Ch-Prefers-Reduced-Motion`	Indicates if the user prefers reduced motion (?0 or ?1).
`Sec-Ch-Prefers-Color-Scheme`	Indicates the preferred color scheme ("light" or "dark").




## Security Fetch `Sec-Fetch`

The **`Sec-Fetch-*` headers** are **security-related headers** that help protect against **cross-site request forgery (CSRF)** and other **cross-origin attacks**. 
They provide information about **how and why** a request was made.

```sh
curl -X GET https://example.com \
    -H "Sec-Fetch-Site: same-origin" \
    -H "Sec-Fetch-Mode: navigate" \
    -H "Sec-Fetch-User: ?1" \
    -H "Sec-Fetch-Dest: document"
```

`Sec-Fetch-Site`	-> Describes the relationship between the request’s origin and the target:
+ `same-origin` Request is from the **same** site (exact domain).
+ `same-site` Request is from a **related** site (same **registrable domain** but different subdomain).
+ `cross-site` Request is from a **completely different site**.
+ `none` No origin information (e.g., direct request in `curl`).

`Sec-Fetch-Mode`	-> Indicates the fetch mode:
+ `navigate` A full page load (browser navigation).
+ `cors` A CORS request (cross-origin resource sharing).
+ `no-cors` A request that does not use CORS (e.g., fetching an opaque resource).
+ `same-origin` A same-origin request.
+ `websocket` A `WebSocket` handshake request.

`Sec-Fetch-User`	-> 
+ Sent only when a user intentionally triggers navigation (e.g., clicking a link). 
+ The value is always `?1` if present.
+ `?1` The request was triggered by a user action (e.g., clicking a link).
+ `(Not sent)`	The request was not triggered by a user directly. 

`Sec-Fetch-Dest`	-> Specifies the destination of the resource being fetched.
+ `document` A full HTML page.
+ `image` An image file (`.png`, `.jpg`, etc.).
+ `script` A JavaScript file.
+ `style` A CSS file.
+ `iframe` An embedded frame.
+ `audio` / `video`	Media files.




## Priority Header

The **`Priority` header** is an **HTTP/2 and HTTP/3 feature** that allows clients (like browsers) to tell the server **which resources are more important** so they can be loaded faster.

It helps browsers **prioritize** important resources, such as:
- Loading **critical scripts** before others.
- Fetching **above-the-fold images** before lower ones.
- Preferring **text content** over **ads**.

```
Priority: u=<urgency>, i, w=<weight>
```
+ `u=<urgency>` **Priority level (0-7)**, lower is **more important** (default is `3`).
+ `i` **Incremental flag** (if present, indicates progressive loading).
+ `w=<weight>` Weight (0-256), used for finer prioritization. (Rarely used)

```
Priority: u=6, i
```
Urgency `6` (lower priority) with `i` for **incremental loading**.

### Why Is `Priority` Important?
**Speeds up page loads** by prioritizing critical content.  
**Optimizes bandwidth** (delays loading non-essential resources).  
**Improves user experience** by loading visible elements first.



## Encoding Preferences

The `Accept-Encoding` header tells the server which **compression formats** the client supports. This helps **reduce data transfer size** and **improve performance**.

```
Accept-Encoding: <encoding>[,<encoding>...]
```

Common Encoding Types:
`gzip` -> Most common compression (widely used).
`deflate` -> Alternative to `gzip`, but less used.
`br` -> `Brotli`, best compression for modern browsers.
`identity` -> No compression (default).
`*` -> Accept any encoding.


**Example**
```
Accept-Encoding: br, gzip
```
Requests **Brotli (`br`) first**, but can accept **Gzip (`gzip`)**.




## Language Preferences

The `Accept-Language` header tells the server **which language(s)** the client prefers for the response.

```
Accept-Language: <language-tag>[;<q=quality>], ...
```
- `<language-tag>` → The **language code** (e.g., `en`, `fr`, `es`).
- `q=<quality>` (optional) → A value between `0` and `1` indicating **priority** (higher means more preferred).

**Examples**

```sh
Accept-Language: en-US,en;q=0.9,fr;q=0.8
```
- **Primary:** American English (`en-US`)
- **Secondary:** General English (`en`)
- **Tertiary:** French (`fr`), slightly less preferred (`q=0.8`)

```sh
Accept-Language: ja, *;q=0.5
```
- **Primary:** Japanese (`ja`).
- **Fallback:** Any language (`*`) but with lower priority (`q=0.5`).





## User-Agent (Identifies the Browser)

The **`User-Agent`** header is an **HTTP request header** that tells the server **who (which browser, OS, or client) is making the request**. 
This helps servers **serve different content** or **apply special handling** based on the client's capabilities.


```
User-Agent: <browser/app> (<system-information>) <engine> <extra-info>
```
**`<browser/app>`** → Name of the browser or application making the request.
**`<system-information>`** → OS, device type, or platform.
**`<engine>`** → The rendering engine (e.g., `WebKit`, `Gecko`).
**`<extra-info>`** → Other relevant details.


**Example**
```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.6778.140 Safari/537.36
```
**`Mozilla/5.0`** → Legacy compatibility string.
**`Windows NT 10.0; Win64; x64`** → Windows 10, 64-bit.
**`AppleWebKit/537.36`** → Uses `WebKit` engine.
**`Chrome/131.0.6778.140`** → Chrome browser version.
**`Safari/537.36`** → Chrome pretends to be Safari for compatibility.


### Why Does the `User-Agent` Header Matter?
**Browser Compatibility** → Websites can adjust their layout based on the browser.  
**Security & Filtering** → Some sites **block bots** or **require specific browsers**.  
**Analytics & Tracking** → Websites track which browsers & devices visit them.  
**Web Scraping & Automation** → Some servers **block requests from bots** (e.g., Python's `requests` library).