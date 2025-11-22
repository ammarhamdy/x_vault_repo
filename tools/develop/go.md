
https://www.kali.org/tools/nuclei/

**Download**: https://go.dev/dl/go1.25.1.linux-amd64.tar.gz
from: https://go.dev/dl/ 

---
# Installation

Add `go` command to your `aliases` on `.bashrc` 
```sh
alias go='/opt/go/bin/go'
```

Add go tools location to your `PATH`
```sh
export PATH=$PATH:$(go env GOPATH)/bin
```

