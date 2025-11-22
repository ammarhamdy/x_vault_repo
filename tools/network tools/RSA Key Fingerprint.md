


When using the `ssh` command, the first prompt asks you to verify the identity of the machine you are logging into.
In most cases, you are going to want to answer `yes`.
While you can check with the administrator of the remote machine to make sure that the RSA key fingerprint is correct, this isn't the purpose of this query.
It is designed for future login attempts.


After you answer `yes`, the RSA key fingerprint of the remote machine is stored on your local system. When you attempt to `ssh` to this same machine in the future, the RSA key fingerprint provided by the remote machine is compared to the copy stored on the local machine. 
If they match, then the username prompt appears.
![[Pasted image 20240227170833.png]]This error could indicate that a rogue host has replaced the correct host. 
Check with the administrator of the remote system. 
If the system were recently reinstalled, it would have a new RSA key, and that would be causing this error.

In the event that this error message is due to a remote machine reinstall, you can remove the `~/.ssh/known_hosts` file from your local system (or just remove the entry for that 
one machine) and try to connect again:
```
sysadmin@localhost:~$ cat ~/.ssh/known_hosts
test ssh-rsa AAAAB3NzaC1yc2EAAAAmIwAAAQEAklOUpkDHrfHY17SbrmTIp/RZ0V4DTxgq9wzd+ohy006SWDSGPA+nafzlHDPOW7vdI4mZ5ew18KL4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSrg0cda3Pbv7kOdJ/MTyBlWXFCRH+Cv3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7BA
t5FaiKoAfncM1Q8x3+2V0Ww71/eIFmb1zuUFljHYTprrX88XypNDvjYNby6vw/Pb0rwprz/Tn
mZAW3UX+PnTPI89ZPmNBLuxyrD2cE86Z/il8b+gw3r3+1nJotmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+ghw==

sysadmin@localhost:~$ rm ~/.ssh/known_hosts

sysadmin@localhost:~$ ssh bob@test
The authenticity of host ‘test (127.0.0.1)’ can’t be established.
RSA key fingerprint is c2:0d:ff:27:4c:f8:69:a9:c6:3e:13:da:2f:47:e4:c9.
Are you sure you want to continue connection (yes/no)? yes
Warning: Permanently added ‘test’ (RSA) to the list of known hosts.
bob@test’s password:
Last login: Fri Oct   4 16:14:39 CDT 2013  from localhost
```

