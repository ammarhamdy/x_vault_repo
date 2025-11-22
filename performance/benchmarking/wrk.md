
**`wrk`**, a high-performance HTTP bench-marking tool, ideal for stress testing HTTP APIs or web servers.

`wrk` is a **modern, multi-threaded** benchmark tool that generates significant load on HTTP servers. 

It's fast, flexible (supports Lua scripts), and more efficient than older tools like `ab`.

---

# Install `wrk`

```bash
sudo apt install wrk
```

----

# Basic Usage

```bash
wrk -t4 -c100 -d30s http://example.com/
```
- `-t4` → 4 threads
- `-c100` → 100 connections (simultaneous users)
- `-d30s` → Run for 30 seconds
- URL → Target endpoint

---

# Testing with POST and Headers (Using Lua)

## Create a Lua script (`post.lua`):
```lua
wrk.method = "POST"
wrk.body   = '{"name":"ChatGPT","type":"AI"}'
wrk.headers["Content-Type"] = "application/json"
wrk.headers["Authorization"] = "Bearer your_token"
```
## Run with the script:
```bash
wrk -t4 -c50 -d20s -s post.lua http://example.com/api
```

---

#  Advanced `wrk` Lua script

**`advanced.lua` — Full Lua Script**
```lua
-- Define global headers
wrk.headers["Content-Type"] = "application/json"
wrk.headers["Authorization"] = "Bearer YOUR_TOKEN_HERE"

-- Pre-generate some data for POST
local names = { "Alice", "Bob", "Charlie", "Diana", "Eve" }
local types = { "admin", "user", "guest" }

-- Setup function (optional)
function setup(thread)
  math.randomseed(os.time() + thread)
end

-- Generate random POST body
function generate_body()
  local name = names[math.random(#names)]
  local type = types[math.random(#types)]
  return string.format('{"name": "%s", "type": "%s"}', name, type)
end

-- Main request function
request = function()
  local rand = math.random()
  
  -- 70% GET /users/:id
  if rand < 0.7 then
    local id = math.random(1, 1000)
    return wrk.format("GET", "/users/" .. id)
  
  -- 30% POST /users
  else
    local body = generate_body()
    return wrk.format("POST", "/users", nil, body)
  end
end
```

| Feature           | Functionality                               |
| ----------------- | ------------------------------------------- |
| `math.random()`   | Chooses which request to send (GET vs POST) |
| `generate_body()` | Builds a dynamic JSON payload               |
| `setup()`         | Seeds randomness for each thread            |
| `wrk.format()`    | Generates raw HTTP requests                 |
| `wrk.headers`     | Sets static headers like Content-Type, Auth |
**How to Run It**
```bash
wrk -t4 -c100 -d30s -s advanced.lua http://example.com
```

