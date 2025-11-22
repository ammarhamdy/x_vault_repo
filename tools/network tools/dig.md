
There may be times when you need to test the functionality of the DNS server that your host is using. 

One way of doing this is to use the `dig` command, which performs queries on the DNS server to determine if the information needed is available on the server.

## ip address of a specific host:
In the following example, the `dig` command is used to determine the IP address of the `example.com` host:
```
root@localhost:~# dig example.com 
; <<>> DiG 9.18.18-0ubuntu2.1-Ubuntu <<>> example.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42070
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;example.com.			IN	A

;; ANSWER SECTION:
example.com.		34519	IN	A	93.184.216.34

;; Query time: 16 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Feb 27 04:49:06 EET 2024
;; MSG SIZE  rcvd: 56

```
+ Note that the response included the IP address of `93.184.216.34`, meaning that the DNS server has the IP address to hostname translation information in its database.
+ If the DNS server doesn't have the requested information, it is configured to ask other DNS servers.
+ If none of them have the requested information, an error message displays:


