

The tool used to automatically download exposed .git repositories from websites if the .git folder is accessible publicly.

An offensive security tool (written in Go) that automatically finds and downloads .git folders from websites if they’re mistakenly left exposed.

**How It Works:**
You point `Gitjacker` to a target website (e.g., https://example.com).
It checks if the `.git` folder is exposed.
If accessible, it clones the repo locally and tries to reconstruct the entire project’s source code.

**Alternatives**
`GitTools` (a set of bash scripts for the same purpose).
`DVCS` Ripper (Perl tool for ripping various version control systems).
`git-dumper` (Python-based).

---

# Installation 
recommended quick method from the repo
```sh
curl -s "https://raw.githubusercontent.com/liamg/gitjacker/master/scripts/install.sh" | bash
```


# Single target
```sh
gitjacker https://example.com/ -o example-com-git
```
`-o` to set an output folder
