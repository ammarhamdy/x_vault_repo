
The `jq` command is a lightweight and flexible command-line tool for working with JSON data.

Think of it as `sed` or `awk` but specifically designed for JSON.

It allows you to parse, filter, transform, and pretty-print JSON with simple and powerful expressions.

---

# Installation 
```sh
sudo apt install jq
```

# Pretty-print JSON
```sh
cat data.json | jq .
```

# Work with arrays

```json
[
  "apple",
  "banana",
  "cherry"
]
```
**Get the first element**
```sh
jq '.[0]' fruits.json
```

```sh
{
  "users": [
    {"name": "Alice", "age": 25},
    {"name": "Bob", "age": 35}
  ]
}
```
**Get the first user’s name:**
```sh
jq '.users[0].name' data.json
```

**Gets the first user's name.**
```
jq '.users[0].name' data.json
```

**Loop through arrays**
```sh
jq '.users[].name' data.json
```

**Filtering with conditions**
```sh
jq '.users[] | select(.age > 30)' data.json
```

# Count elements
```sh
jq '.users | length' data.json
```

# URL encoder

```sh
echo "hello world & foo=bar" | jq -sRr @uri
```
**`-s` (slurp)**:
+ Instead of processing input line by line, `jq` reads the **entire input as one string**.

**`-R` (raw input)**: 
+ Tells `jq` to treat the input as **raw text** instead of JSON. 
+ So it won’t expect `{}` or `[]`, just plain text.

**`-r` (raw output)**: 
+ Makes `jq` output plain strings 
+ Without quotes or JSON formatting.

**`@uri`**: 
+ A built-in `jq` **string filter** that encodes the input as a **percent-encoded URI component** (aka URL encoding). 
+ For example, spaces → `%20`, `?` → `%3F`.

