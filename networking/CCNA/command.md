
### give ip to router:
- type on CLI:
```
	> ena
	# configure terminal
	# interface g0/0
	# ip address 192.168.1.10 255.255.255.0
	# no shutdown
```


### create user name and password to console for router:
- type on CLI:
```
	> en
	# configure t
	# username anyname privilege 15 password anypassword
	# line console 0
	# login local
	# do write
```


### make ftp server:
- create server
- from services tap choose your service "FTP".
- create yourname and password.
- delete all files on that server or not.


### copy configration file from router to FTP server:
- open CLI on router and type:
	- enable
	- configure terminal
	- ip ftp username saved_user_name_on_FTP_server
	- ip ftp password saved_password_on_FTP_server
	- exit


### enter to server from route:
- type on CLI:
	- enable
	- configure terminal
	- ip ftp username ....
	- ip ftp password ....
	- exit
- copy from fpt  to router server:
	- in enable mode:
	- copy ftp startup-config
	- Address or name of remote host ? the_server_ip+address
	- Source filename ? file_name
	- reload
	- System configuration has been modified. Save? [yes/no]: no




### create loop back on Router.
- type on CLI:
```
	> ena
	# config t 
	# interface loopback 0
	# ip address 1.1.1.1 255.255.255.0
	# no shutdown
```
- make it default getway:
```
	# ip default-getway 1.1.1.1
```



### open telnet on router:
- type on CLI:
```
	# username A privilege 15 password 123
	# line vty 0 15
	# login local
```
- on CMD from any pc:
```
	> telnet 192.168.1.1 //the router ip
```


### open SSH on router:
- type on CLI:
```
	# ip domain-name nti.com
	# username $name privilege 15 password $password
	# crypto key generate rsa
	# line vty 0 15
	# login local
	# transport input ssh
```
- on CMD from any PC:
```
	> ssh -L $name 192.169.1.1
```


### Add ip address to routing table (static routing):
- type on CLI:
```
	# ip route 192.168.1.1 255.255.255.0 g0/0
```


### Show:
- type on CLI:
```
	# show ip protocols
	# show ip interface brief
	# show ip running-config
	# show ip interface g0/0
```


### Give ip to vlan on switch:
```
	# interface vlan 1
	# ip address 192.168.1.1 255.255.255.0
```


### Create vlan up interface on switch:
```
	# interfaca f0/1
	# switchport mode access
	# switchprot access vlan $number_of_vlan 
```


### Chnage interface to trunk mode on switch:
```
	# interface f0/1
	# switchport mode trunk
	# switchport trunk encapsulation dot1q 
```


### Change native vlan up interface on switch:
```
	# switchport trunk native vlan $number_of_vlan 
```



