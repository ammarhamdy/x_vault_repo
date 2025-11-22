

The `ssh` command allows you to connect to another machine across the network, log in and then perform tasks on the remote machine.

If you only provide a machine name or IP address to log into, the `ssh` command assumes you want to log in using the same username that you are currently logged in as.

To use a different username, use the syntax:
```
username@hostname
```

```
root@localhost:~# ssh bob@test
```

