

In its simplest form, the `host` command works with DNS to associate a hostname with an IP address. 

As used in a previous example, example.com is associated with the IP address of `192.168.1.2`:

```bash
am@ubuntu:~$ host example.com
example.com has address 93.184.216.34
example.com has IPv6 address 2606:2800:220:1:248:1893:25c8:1946
example.com mail is handled by 0 .

```


The `host` command can also be used in reverse if an IP address is known, but the domain name is not.
```
root@localhost:~# host 192.168.1.2  
```


Other options exist to query the various aspects of a DNS such as a `CNAME` canonical name -alias:
```
root@localhost:~# host -t CNAME example.com
example.com has no CNAME record        
```


A comprehensive list of DNS information regarding example.com can be found using the `-a` all option:
```
root@localhost:~# host -a example.com 
```


