

```bash
cd opt
sudo git clone https://github.com/HashPals/Name-That-Hash.git
```

**Run**
```bash
PYTHONPATH="/opt/Name-That-Hash" python3 -m name_that_hash --text '5f4dcc3b5aa765d61d8327deb882cf99'
```

**Alias on .bashrc**
```bash
alias nth='PYTHONPATH="/opt/Name-That-Hash" python3 -m name_that_hash'
```

**Use**
```bash
nth --text '5f4dcc3b5aa765d61d8327deb882cf99'
```

**Example**
```bash
nth -f hashes.txt
```
The tool will try to identify each hash line-by-line.


|Option|Description|
|---|---|
|`-f FILE`|Input file of hashes|
|`--quiet`|Suppress prettified output (machine-friendly)|
|`--version`|Show version|
|`--no-pretty`|Raw table output (useful for scripting)|
