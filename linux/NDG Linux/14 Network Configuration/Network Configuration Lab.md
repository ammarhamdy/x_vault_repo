

## `ifconfig`:
+ In order to determine your Internet Protocol (IP) address, execute the `ifconfig` command:
+ The output shows two main blocks of information. 
	+ The first block, indented by `eth0`, reflects information about your first Ethernet network card. 
	+ The second block, indented by `lo`, reflects information about the loopback or internal network interface.


Verify that the IP address `127.0.0.1` has an entry in the `/etc/hosts` file:
```
grep 127.0.0.1 /etc/hosts
```
The output should appear as follows, defining the `localhost` names:
```
sysadmin@localhost:~$ grep 127.0.0.1 /etc/hosts                                 
127.0.0.1       localhost
```


## Well known port numbers:
+ Well-known ports are the port numbers in the range of 0-1023, typically used by system processes to provide network services. 
+ A list of service names and associated port numbers can be found in the `/etc/services` file.