

## `shutdown` command:
```
shutdown [OPTIONS] TIME [MESSAGE]
```
- Unlike other commands used to bring the system down, the `shutdown` command requires a time argument specifying when the shutdown should begin. 
- Formats of this time argument can be the word `now`, a time of day in the format `hh:mm` or the number of minutes to delay in the format `+minutes`.
- The clock on our system may be set to a different timezone than the one in which you are located. 


## `date` command:
+ To check the time in the terminal, use the `date` command. 
+ The default format of the `date` command output is as follows:
```
weekday month day hour:minute:second UTC year
```
+ The letters `UTC` present in the output indicates that the time is being displayed as Universal Coordinated Time.
```sh
root@localhost:~# shutdown +1 "Goodbye World!"
```
```sh
root@localhost:~# date                                                      
Sat Oct  3 22:15:58 UTC 2020 
root@localhost:~# shutdown 01:51            
                                                                                
Broadcast message from sysadmin@localhost                                       
        (/dev/pts/0) at 1:50 ...                                              
                                                                                
The system is going down for maintenance in 1 minute!

Broadcast message from sysadmin@localhost                                       
        (/dev/pts/0) at 1:51 ...                                              
                                                                                
The system is going down for maintenance NOW! 
```


