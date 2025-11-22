


The `ss` command is designed to show socket statistics and supports all the major packet and socket types. 
Meant to be a replacement for and to be similar in function to the `netstat` command, it also shows a lot more information and has more features.


## What `ss` used for:
The main reason a user would use the `ss` command is to view what connections are currently established between their local machine and remote machines, statistics about those connections, etc.
![[Pasted image 20240227043740.png]]
The output is very similar to the output of the `netstat` command with no options. The columns above are:

|                 |                                                                     |
| --------------- | ------------------------------------------------------------------- |
| `Netid`         | The socket type and transport protocol                              |
| `State`         | Connected or Unconnected, depending on protocol                     |
| `Recv-Q`        | Amount of data queued up for being processed having been received   |
| `Send-Q`        | Amount of data queued up for being sent to another host             |
| `Local Address` | The address and port of the local host’s portion of the connection  |
| `Peer Address`  | The address and port of the remote host’s portion of the connection |


## `ss -s`:
The format of the output of the `ss` command can change dramatically, given the options specified, such as the use of the `-s` option, which displays mostly the types of sockets, statistics about their existence and numbers of actual packets sent and received via each socket type
```
am@ubuntu:~$ ss -s
Total: 1014
TCP:   11 (estab 4, closed 1, orphaned 0, timewait 0)

Transport Total     IP        IPv6
RAW	  1         0         1        
UDP	  9         6         3        
TCP	  10        9         1        
INET	  20        15        5        
FRAG	  0         0         0     
```


