
**Hey**, a simple HTTP load generator.

**Hey** is a CLI tool written in Go, great for benchmarking web applications and APIs. It's easier to use than `ab`, supports HTTP/1.1, and is cross-platform.

**Installation**
```bash
go install github.com/rakyll/hey@latest
```

**Basic Usage**
```bash
hey -n <requests> -c <concurrency> <URL>
```

---
# Common Options

|Flag|Description|
|---|---|
|`-n`|Number of requests to run.|
|`-c`|Number of concurrent workers (users).|
|`-m`|HTTP method (`GET`, `POST`, etc).|
|`-H`|Custom HTTP header (can be repeated).|
|`-d`|Raw request body data.|
|`-D`|File containing request body.|
|`-A`|Set User-Agent string.|
|`-T`|Content-Type header.|
|`-t`|Timeout in seconds.|
|`-x`|Proxy URL (e.g., `http://localhost:8080`).|

---

# Examples

## Post request
```bash
hey -n 500 -c 10 -m POST -H "Content-Type: application/json" -d '{"name":"John"}' http://localhost:8080/api
```

## Post request with file input
```bash
hey -n 500 -c 10 -m POST -H "Content-Type: application/json" -D ./data.json http://localhost:8080/api
```

