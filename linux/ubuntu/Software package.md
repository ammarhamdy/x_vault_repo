
# Package manager
https://packages.ubuntu.com/

## Listing

```
snap list
```

```
apt list | grep <name>
```

```
dpkg -l | grep <name>
```

---
# Repository

A **repository** on Ubuntu ___is a centralized storage location where software packages___ are stored and managed. 

These repositories are used by package managers like `apt` to download, install, and update software.

## Types of Repositories on Ubuntu

**Main:** 
	Contains officially supported open-source software, maintained by Canonical.

**Restricted:** 
	Includes proprietary drivers and software that are essential but not open-source (e.g., NVIDIA drivers).

**Universe:** 
	Community-maintained free and open-source software.

**Multiverse:**
	Software that is not free or has licensing restrictions.

**Third-Party Repositories:**
	Maintained by external developers or organizations, such as PPAs (Personal Package Archives).


## Repository Locations

**Repositories are configured in the file:**
`/etc/apt/sources.list` or `/etc/apt/sources.list.d/ubuntu.sources`
```
cat /etc/apt/sources.list.d/ubuntu.sources
Types: deb
URIs: http://eg.archive.ubuntu.com/ubuntu/
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: http://security.ubuntu.com/ubuntu/
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```
+ **deb**: Denotes a binary package repository.
+ **URIs**: The repository URIs.
+ **main**, **restricted**, **universe**, **multiverse**: Components of the repository.

**Update Package List**
To ensure your system has the latest information about available software:
```
sudo apt update
```

**Add a Repository**
For example, to add a `PPA`:
```
sudo add-apt-repository ppa:<repository-name> sudo apt update
```

**List Current Repositories**
```
apt policy
```

**Remove a Repository**
Manually edit the `/etc/apt/sources.list.d/ubuntu.sources` file or use:
```
sudo add-apt-repository --remove ppa:<repository-name>
```

**Show information**
```
pat-cache show commmix 
```

**Fix broken installation**
```
sudo apt --fix-broken install
```
