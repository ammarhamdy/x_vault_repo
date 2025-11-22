
`sshpass` is a small utility that lets you provide an SSH password non-interactively (useful for quick scripts or one-off automation).

# Install `sshpass`
```sh
sudo apt install sshpass
```


# Basic usage

Using `-p` (password on command line) — _least safe_
```sh
sshpass -p 'MySecretPassword' ssh user@host.example.com
```

Using `-e` (read password from environment variable) — slightly better
```sh
export SSHPASS='MySecretPassword'
sshpass -e ssh user@host.example.com
```

# Run a remote command

```sh
sshpass -p 's3cr3t' ssh user@172.16.10.13 'uptime && whoami'
```

Automatically accept an unknown host key (INSECURE)
+ If you want to automatically accept a new host key (`Are you sure you want to continue?` prompt)
+ Combine `ssh` option `-o StrictHostKeyChecking=no`.
```sh
sshpass -p 's3cr3t' ssh -o StrictHostKeyChecking=no user@172.16.10.13
```



