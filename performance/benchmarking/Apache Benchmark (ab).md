

**Best for:** Quick sanity checks or testing static pages
**Pros:**
- Pre-installed on many systems
- Very easy to use
**Cons:**
- Only supports HTTP/1.0
- No support for JS, cookies, or complex flows
- Limited metrics


---
# Basic Command Syntax

```sh
ab -n <total_requests> -c <concurrent_users> <url>
```

```sh
ab -n 1000 -c 100 https://yourwebsite.com/
```
- Make 1000 total requests.
- 100 users at the same time (concurrency).


**Important Options in** `ab`:
`-n`	Total number of requests to perform
`-c`	Number of multiple requests to perform at a time (concurrency)
`-t`	Instead of -n, run test for X seconds
`-p`	Send POST data from a file
`-T`	Content-Type header for POST/PUT requests
`-A`	HTTP Basic Authentication username:password
`-H`	Add custom HTTP headers (like Authorization, Cookies)
`-k`	Use HTTP KeepAlive (persistent connections)
`-r`	Don't exit on socket receive errors
`-g`	Output results in gnuplot format (for graphing)
`-v`	Set verbosity level (debug output (2 shows headers))
`-x`  Output results in CSV format
`-m`  HTTP method to use (`GET`, `POST`, etc.)


```sh
ab -n 50 -c 5 -p post_data.json -T application/json http://example.com/api/
```


---

# 📊 **Reading the Output**

Key parts of the result:

- `Requests per second`: Throughput of the server

- `Time per request`: Latency per request (mean time)

- `Percentage of the requests served within a certain time`: Useful for response time percentiles

---
# Common usage

## POST request with JSON
```bash
ab -n 100 -c 10 -p post_data.json -T application/json http://example.com/api/
```
Where `post_data.json` contains something like:
```json
{"name": "ChatGPT", "type": "AI"}
```

## Authenticated GET request
```bash
ab -n 50 -c 5 -H "Authorization: Bearer YOUR_TOKEN" http://example.com/protected/
```

## Benchmark for a duration
```bash
ab -t 30 -c 5 http://example.com/
```
This will run for 30 seconds regardless of how many requests are completed.


----
# `ab` vs `wrk` vs `k6`

| Feature              | **Apache Benchmark (ab)**    | **wrk**                       | **k6**                                  |
| -------------------- | ---------------------------- | ----------------------------- | --------------------------------------- |
| **Ease of Use**      | 🗸 Very simple CLI           | 🗸 Simple CLI                 | ! More complex, scripting required     |
| **Performance**      | ! Lower                     | 🗸 Very high                  | 🗸 Good, but lower than `wrk`           |
| **Scripting**        | 𐄂 No                        | ! Lua-based                  | 🗸 JavaScript-like scripting            |
| **HTTP Version**     | HTTP/1.0 only                | HTTP/1.1, HTTP/2 (some forks) | HTTP/1.1, HTTP/2, HTTP/3                |
| **SSL Support**      | 🗸 Yes                       | 🗸 Yes                        | 🗸 Yes                                  |
| **Concurrency**      | 🗸 Yes (`-c`)                | 🗸 Yes                        | 🗸 Yes                                  |
| **Realistic Load**   | 𐄂 No (no browser emulation) | 𐄂 No                         | 🗸 Simulates real user flows            |
| **Graphical Output** | 𐄂 No                        | 𐄂 No                         | 🗸 Yes (via dashboard, reports)         |
| **Platform**         | Linux/macOS (CLI)            | Linux/macOS (CLI)             | Cross-platform (CLI + Cloud)            |
| **Good For**         | Quick tests, simple GETs     | High performance, load stress | Load testing with scenarios and metrics |