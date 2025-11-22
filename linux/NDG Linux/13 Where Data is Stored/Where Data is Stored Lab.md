
## `proc` directory:

The `/proc` directory also contains information about the operating system and its hardware in files like `/proc/cpuinfo`, `/proc/meminfo` and `/proc/devices`.

The `/proc/sys` subdirectory contains pseudo files that can be used to alter the settings of the running kernel. Since these files are not "real" files, an editor should not be used to change them; instead you should use either the `echo` or the `sysctl` command to overwrite the contents of these files. For the same reason, do not attempt to view these files in an editor, but use the `cat` or `sysctl` command instead.

For permanent configuration changes, the kernel uses the `/etc/sysctl.conf` file. Typically, this file is used by the kernel to make changes to the /proc files when the system is starting up.


View the `/proc/cmdline` file to see what arguments were passed to the kernel at boot time:

```
cat /proc/cmdline
```


---
#  Managing Processes

```
ping localhost > /dev/null
```
The output of the `ping` is being redirected to the `/dev/null` file (which is commonly known as the bit bucket).
Notice that the terminal appears to hang up at this command.
Next, to start the same process in the background, type:
```
ping localhost > /dev/null &
```


```
root@localhost:~# ping localhost > /dev/null &                                  
[1] 107
```
Notice that the previous command returns the following information:
This means that this process has a job number of 1 (as demonstrated by the output of `[1]`) and a Process ID (PID) of `107`. Each terminal/shell will have unique job numbers. The PID is system-wide; each process having a unique ID number.


To see which commands are running in the current terminal, type the following command:
```
jobs
```
Your output should be similar to the following:
```bash
root@localhost:~# jobs                                                          
[1]+  Running                 ping localhost > /dev/null &
```
bring the first command to the foreground by typing the following:
```
fg %1
```
To suspend (pause) the process and regain control of the terminal, type **Ctrl**-**Z**
To have this process continue executing in the background, execute the following command:
```
bg %1
```
Using the job number, stop the third `ping` command with the `kill` command and verify it was stopped executing the `jobs` command:
```
kill %3
```
Finally, you can stop all of the `ping` commands with the `killall` command. After executing the `killall` command, wait a few moments, and then run the `jobs` command to verify that all processes have stopped:
```
killall ping
```


```bash
am@ubuntu:~$ ping localhost > ping1 &
[1] 8490
am@ubuntu:~$ ping localhost > ping2 &
[2] 8491
am@ubuntu:~$ jobs
[1]-  Running                 ping localhost > ping1 &
[2]+  Running                 ping localhost > ping2 &
am@ubuntu:~$ kill %1
am@ubuntu:~$ jobs
[1]-  Terminated              ping localhost > ping1
[2]+  Running                 ping localhost > ping2 &
am@ubuntu:~$ fg %1
bash: fg: %1: no such job
am@ubuntu:~$ fg %2
ping localhost > ping2
^Cam@ubuntu:~$ 
```


---
# Use Top to View Processes


The `top` command is an interactive program, which means that you can issue commands within the program. You will use the `top` command to kill the `ping` processes. First, type the letter **k**. Notice a prompt has appeared

At the `PID to kill:` prompt, type the PID of the first running `ping` process, then press **Enter**.

There are several different numeric values that can be sent to a process. 
These are predefined values, each with a different meaning. If you want to learn more about these values, type `man kill` in a terminal window.

The prompt indicates that the default signal is the terminate signal indicated by `SIGTERM` or the number `15`.

![[lab11_3.gif]]
prompt, use a value of `9` instead of accepting the default of `15`. Press **Enter** to accept the entry.
The kill signal `9` or `SIGKILL` is a "forceful" signal that cannot be ignored, unlike the default value of `15`. Notice that all references to the `ping` command are now removed from `top`.



---
# Use pkill and kill To Terminate Processes


To begin, type the following commands in the terminal:
```
sleep 888888 &
sleep 888888 &
```
The `sleep` command is typically used to pause a program (shell script) for a specific period of time.
In this case it is used just to provide a command that will take a long time to run.
Now, use the `kill` command to stop the first instance of the `sleep` command by typing the following (substitute PID with the process id of your first `sleep` command). 
Also, execute `jobs` to verify the process has been stopped:
```
ps
kill PID
jobs
```
Next, use the `pkill` command to terminate the remaining `sleep` command, using the name of the program rather than the PID:
```bash
pkill -15 sleep
```




---
# Using ps to Select and Sort Processes


The `ps` command can be used to view processes. By default, the `ps` command will only display the processes running in the current shell.
Execute the `ps` command using the option `-e`, so all processes are displayed.
```
ps -e
```
Use the `ps` command with the `-o` option to specify which columns to output.
```
ps -o pid,tty,time,%cpu,cmd
```
```
root@localhost:~# ps -o pid,tty,time,%cpu,cmd                                   
  PID TT           TIME %CPU CMD                                                
    1 ?        00:00:00  0.0 /bin/bash /init                                    
   51 ?        00:00:00  0.0 /bin/login -f                                      
   90 ?        00:00:00  0.0 su                                                 
   91 ?        00:00:00  0.0 bash                                               
  138 ?        00:00:00  0.0 ping localhost                                     
  141 ?        00:00:00  0.0 ps -o pid,tty,time,%cpu,cmd
```
Use the `--sort` option to specify which column(s) to sort by. By default, a column specified for sorting will be in ascending order, this can be forced with placing a plus `+` symbol in front of the column name. To specify a descending sort, use the minus `-` symbol in front of the column name.
Sort the output of `ps` by `%mem`:
```bash
ps -o pid,tty,time,%mem,cmd --sort %mem
```


---
# Viewing System Logs


There are two daemons that handle log messages: the `syslogd` daemon and the `klogd` daemon.
Typically you don't need to worry about `klogd`; it only handles kernel log messages and it sends its log information to the `syslogd` daemon.

Messages that were generated by the kernel at boot time are stored in the `/var/log/dmesg` file. 
The `dmesg` command allows viewing of current kernel messages, as well as providing control of whether those messages will appear in a terminal console window.

The main log file that is written to by `syslogd` is `/var/log/`messages.

In addition to the logging done by `syslogd`, many other processes perform their own logging. 
Some examples of processes that do their own logging include the Apache web server (log file resides in the `/var/log/httpd` directory), the Common Unix Printing System (`/var/log/cups`) and the `auditd` daemon (`/var/log/audit`).


System logs are stored in the `/var/log` directory. List the files in this directory:
```
ls /var/log
```


Each log file represents a service or feature. For example, the `auth.log` file displays information regarding authorization or authentication, such as user login attempts. New data is stored at the bottom of the file. Execute the following commands to see an example:
```
ssh localhost
tail -5 /var/log/auth.log
```