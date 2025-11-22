
https://www.kali.org/tools/amass/
https://github.com/owasp-amass/amass/blob/master/doc/tutorial.md

---
# Different Modes

Amass has several subcommands:

- `enum` → Subdomain enumeration

- `viz` → Visualize the discovered attack surface

- `db` → Interact with the Amass database

- `track` → Monitor changes over time

- `intel` → Discover root domains, ASN info, and netblocks

- `dns` → Perform DNS enumeration

- `help` → Get help


---
# Subdomain enumeration:
```sh
amass enum -d example.com
```
Passive enumeration (no DNS resolution):
```sh
amass enum -passive -d example.com
```
Active enumeration (resolves DNS records):
```sh
amass enum -active -d example.com
```
Save results to a file:
```sh
amass enum -d example.com -o results.txt
```
ASN-based discovery:
```sh
amass intel -asn 13335
```

# Visualization
You can generate a graph of discovered assets:
```sh
amass viz -d3 -o amass_graph.db
```