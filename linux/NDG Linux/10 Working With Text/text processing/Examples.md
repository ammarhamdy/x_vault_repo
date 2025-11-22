

# Ping all ips in my network

**Data:**
```sh
⸢~/tempo⸥ cat main_codlop_netdiscover 
 192.168.1.44    dc:4a:3e:75:ba:77      8     480  Hewlett Packard                                    
 192.168.1.1     30:42:40:b7:11:5c      1      42  zte corporation                                    
 192.168.1.2     60:a4:b7:e5:66:ce      1      60  TP-Link Corporation Limited                        
 192.168.1.3     dc:4a:3e:75:ba:77      1      60  Hewlett Packard                                    
 192.168.1.17    00:18:ae:da:a7:df      1      60  TVT CO.,LTD                                        
 192.168.1.29    48:0f:cf:3b:60:3c      1      60  Hewlett Packard                                    
 192.168.1.38    dc:4a:3e:88:a5:a4      1      60  Hewlett Packard                                    
 192.168.1.39    dc:4a:3e:69:1e:53      1      60  Hewlett Packard                                    
 192.168.1.85    a0:8c:fd:df:7a:05      1      60  Hewlett Packard                                    
 192.168.1.12    06:da:35:df:aa:ea      1      42  Unknown vendor                                     
 192.168.1.121   c4:34:6b:71:ac:cd      1      60  Hewlett Packard                                    
 192.168.1.26    a6:a7:98:2c:ad:fc      2      84  Unknown vendor                                     
 192.168.1.30    92:3c:b7:8c:d8:89      1      42  Unknown vendor                                     
 192.168.1.27    34:e6:ad:b0:ef:af      1      42  Intel Corporate                                    
 192.168.1.45    00:0c:a1:10:12:f3      1      42  SIGMACOM Co., LTD.    
```

**Extract first column:**
```sh
⸢~/tempo⸥ cut -c 1-15 main_codlop_netdiscover 
 192.168.1.44  
 192.168.1.1   
 192.168.1.2   
 192.168.1.3   
 192.168.1.17  
 192.168.1.29  
 192.168.1.38  
 192.168.1.39  
 192.168.1.85  
 192.168.1.12  
 192.168.1.121 
 192.168.1.26  
 192.168.1.30  
 192.168.1.27  
 192.168.1.45  
```

**Remove trailing spaces:**
```sh
cut -c 1-15 main_codlop_netdiscover | tr -d ' '
```

**Replace newline with other character:**
```sh
cut -c 1-15 main_codlop_netdiscover | tr -d ' ' | tr '\n' ' ' 
192.168.1.44 192.168.1.1 192.168.1.2 192.168.1.3 192.168.1.17 192.168.1.29 192.168.1.38 192.168.1.39 192.168.1.85 192.168.1.12 192.168.1.121 192.168.1.26 192.168.1.30 192.168.1.27 192.168.1.45
```

**Convert to array:**
```sh
⸢~/tempo⸥ readarray ips <<< $(cut -c 1-15 main_codlop_netdiscover | tr -d ' ') 
```

**Print array:**
```sh
⸢~/tempo⸥ printf '%s\n' ${ips[@]} 
```

**Loop for the array:**
```sh
⸢~/tempo⸥ for i in "${ips[@]}"; do echo $i; done
```

**Ping all:**
```sh
⸢~/tempo⸥ for i in "${ips[@]}"; do ping $i -c 3 -W 3; done
```
`-c` for count.
`-W` for time out in second.



---
