---
layout: post
title: sftp uqgec localhost port number for pi and pizero devices
---

### hydrogeologgermini (currently working on the roof for the stanwell project)
```bash
   ssh pi@localhost -p 1992
```
Telstra 3g usb modem is used to provide internet
Pi zero is working as wifi router to provide internet for photon weather station
   

### hydrogeologger (the pi 3 B+ sitting on chenming's desk)
```bash
   ssh pi@localhost -p 1993
```
the pi 3 B+ connect to uq wifi
the pi is working as wifi router

### hydrogeologgermini (deployed in gelita)

```bash
   ssh pi@localhost -p 20007
```

Telstra 3g usb modem is used to provide internet
Pi zero is working as wifi router to provide internet to photon weather station

### hydrogeologgermini (deployed in gelita) 

```bash
   ssh pi@localhost -p 20003
```
Autossh is setup in Ximing's mango
Telstra 3g usb modem is used to provide internet

### number of ports required by each autossh

autossh is been called by the following command:

```bash
AUTOSSH_DEBUG=7 autossh -M 20000 -f -o"ServerAliveInterval 6000" -o "ServerAliveCountMax 10" -o "ExitOnForwardFailure=yes" -i ~/.ssh/id_rsa_sftp_uqgec -N sftp@xxx.xx.xx.xx -R 2003:localhost:5901 -R 1992:localhost:22 -C  >>/home/pi/autossh_debug  
```

in the host, the following ports are used for stanwell. 20000,20001, 2003,1992

so the next system should be configured as

```bash
AUTOSSH_DEBUG=7 autossh -M 20002 -f -o"ServerAliveInterval 6000" -o "ServerAliveCountMax 10" -o "ExitOnForwardFailure=yes" -i ~/.ssh/id_rsa_sftp_uqgec -N sftp@xxx.xx.xx.xx -R 2004:localhost:5901 -R 1993:localhost:22 -C  >>/home/pi/autossh_debug  
```
the following ports are used for stanwell. 20002,20003, 2004,1993

### pi@grange1 (grange_type_b)

```bash
   ssh pi@localhost -p 20001
```

### pi@grange2 (grange_type_a & grange_type_D)

```bash
   ssh pi@localhost -p 20002
```
### pi@grange4 (grange_5_column4 & grange_3_column5)

```bash
   ssh pi@localhost -p 20004
```

### pi@grange5 (grange_4_column6)

```bash
   ssh pi@localhost -p 20005
```
### TO190426 some knowledge about the autossh

```bash
#!/bin/bash
sleep 120
#ssh -NTf -i /home/pi/.ssh/id_rsa_sftp_uqgec -R 1992:localhost:22 -R 2003:localhost:5901 sftp@144.6.225.24
#AUTOSSH_DEBUG=7 autossh -M 20000 -f -o"ServerAliveInterval 6000" -o "ServerAliveCountMax 10" -i ~/.ssh/id_rsa_sftp_uqgec -N sftp@144.6.225.24 -R 2003:localhost:5901 -R 1992:localhost:22 -C >>/home/pi/autossh_deb
#AUTOSSH_DEBUG=7 autossh -M 20000 -f -o"ServerAliveInterval 6000" -o "ServerAliveCountMax 10" -o "ExitOnForwardFailure=yes" -i ~/.ssh/id_rsa_sftp_uqgec -N sftp@144.6.225.24 -R 2003:localhost:5901 -R 1992:localhost:22 -C  >>/home/pi/autossh_debug
AUTOSSH_DEBUG=1 AUTOSSH_LOGLEVEL=7 AUTOSSH_LOGFILE=/home/pi/autossh_debug_2 autossh -M 20000 -f -o"ServerAliveInterval 6000" -o "ServerAliveCountMax 10"  -i ~/.ssh/id_rsa_sftp_uqgec -N sftp@144.6.225.24 -R 2003:localhost:5901 -R 1992:localhost:22 -C
#https://serverfault.com/questions/626461/autossh-does-not-kill-ssh-when-link-down
#AUTOSSH_DEBUG=7 autossh -M 20000 -f -o"ServerAliveInterval 60" \
#         -o "ServerAliveCountMax 2" \
#         -o "ClientAliveInterval 60" \
#         -o "ClientAliveCountMax 2" \
#         -o "ExitOnForwardFailure=Yes"\
#         -i ~/.ssh/id_rsa_sftp_uqgec \
#         -N sftp@144.6.225.24 \
#         -R 2003:localhost:5901 -R 1992:localhost:22 -C >>/home/pi/autossh_deb
#TO190426
# it is found in stanwell instance that with -o "ExitOnForwardFailure=Yes", autossh may fail to establish a ssh session, when i remove it, ssh re establish
# never see autossh_Debug=7, but =1 is common
## https://www.mankier.com/1/autossh
#AUTOSSH_DEBUG=1 AUTOSSH_LOGFILE=log_file AUTOSSH_LOGLEVEL=7 autossh -f -M monitor_port -v -E ssh_log_file ssh_command

```
now checking some details


```
pi@stanwellmini:~/script $ cat ~/autossh_debug_2
2019/04/26 14:22:10 autossh[1016]: checking for grace period, tries = 0
2019/04/26 14:22:10 autossh[1016]: starting ssh (count 1)
2019/04/26 14:22:10 autossh[1016]: ssh child pid is 1018
2019/04/26 14:22:10 autossh[1016]: check on child 1018
2019/04/26 14:22:10 autossh[1016]: set alarm for 600 secs
2019/04/26 14:22:10 autossh[1018]: execing /usr/bin/ssh
2019/04/26 14:32:25 autossh[1016]: timeout polling to accept read connection
2019/04/26 14:32:25 autossh[1016]: port down, restarting ssh
2019/04/26 14:32:25 autossh[1016]: checking for grace period, tries = 0
2019/04/26 14:32:25 autossh[1016]: starting ssh (count 2)
2019/04/26 14:32:25 autossh[1016]: ssh child pid is 1168
2019/04/26 14:32:25 autossh[1016]: check on child 1168
2019/04/26 14:32:25 autossh[1016]: set alarm for 600 secs
2019/04/26 14:32:25 autossh[1168]: execing /usr/bin/ssh
2019/04/26 14:42:40 autossh[1016]: timeout polling to accept read connection
2019/04/26 14:42:40 autossh[1016]: port down, restarting ssh
2019/04/26 14:42:40 autossh[1016]: checking for grace period, tries = 0
2019/04/26 14:42:40 autossh[1016]: starting ssh (count 3)
2019/04/26 14:42:40 autossh[1016]: ssh child pid is 1299
2019/04/26 14:42:40 autossh[1016]: check on child 1299
2019/04/26 14:42:40 autossh[1016]: set alarm for 600 secs
2019/04/26 14:42:40 autossh[1299]: execing /usr/bin/ssh

pi@stanwellmini:~/script $ ps aux|grep ssh
root       382  0.0  1.4  10188  5312 ?        Ss   14:20   0:00 /usr/sbin/sshd -D
pi         699  0.0  0.2   3780   992 ?        Ss   14:20   0:00 /usr/bin/ssh-agent x-session-manager
pi         808  0.0  0.2   3780   980 ?        Ss   14:20   0:00 /usr/bin/ssh-agent -s
pi        1016  0.0  0.3   1816  1232 ?        Ss   14:22   0:00 /usr/lib/autossh/autossh -M 20000    -oServerAliveInterval 6000 -o ServerAliveCountMax 10 -i /home/pi/.ssh/id_rsa_sftp_uqgec -N sftp@144.6.225.24 -R 2003:localhost:5901 -R 1992:localhost:22 -C
pi        1018  0.2  1.3   9248  5180 ?        S    14:22   0:00 /usr/bin/ssh -L 20000:127.0.0.1:20000 -R 20000:127.0.0.1:20001 -oServerAliveInterval 6000 -o ServerAliveCountMax 10 -i /home/pi/.ssh/id_rsa_sftp_uqgec -N -R 2003:localhost:5901 -R 1992:localhost:22 -C sftp@144.6.225.24
root      1021  0.0  1.5  11508  5704 ?        Ss   14:22   0:00 sshd: pi [priv]
pi        1030  0.1  1.0  11508  3812 ?        S    14:22   0:00 sshd: pi@pts/0
pi        1148  0.0  0.5   4364  2100 pts/1    S+   14:28   0:00 grep --color=auto ssh
```

S means it is now sleeping

i think for the next stage, we could simply kill autossh, clear the port, and reconnect. also notice -oServerAliveInterval 6000 -o ServerAliveCountMax 10, the moment to check the result is every 600 second according to the log

the newest setup is now as below TO 20190429:

```
sleep 120
AUTOSSH_DEBUG=1 AUTOSSH_LOGLEVEL=7 AUTOSSH_LOGFILE=/home/pi/autossh_debug_2 autossh -M 20001 -f -o "ServerAliveInterval=12000" -o "ServerAliveCountMax=10"  -o "ExitOnForwardFailure=Yes" -i ~/.ssh/id_rsa_sftp_uqgec -N sftp@144.6.225.24 -R 1992:localhost:22 -C 
```

Below is the result from ps:

```
root       383  0.0  1.3  10188  5248 ?        Ss   11:43   0:00 /usr/sbin/sshd -D
pi         700  0.0  0.2   3780  1052 ?        Ss   11:44   0:00 /usr/bin/ssh-agent x-session-manager
pi         810  0.0  0.2   3780   980 ?        Ss   11:44   0:00 /usr/bin/ssh-agent -s
pi        1026  0.0  0.3   1816  1284 ?        Ss   11:45   0:00 /usr/lib/autossh/autossh -M 20001    -o ServerAliveInterval=12000 -o ServerAliveCountMax=10 -o ExitOnForwardFailure=Yes -i /home/pi/.ssh/id_rsa_sftp_uqgec -N sftp@144.6.225.24 -R 1992:localhost:22 -C
pi        1028  0.0  1.3   9248  5284 ?        S    11:45   0:01 /usr/bin/ssh -L 20001:127.0.0.1:20001 -R 20001:127.0.0.1:20002 -o ServerAliveInterval=12000 -o ServerAliveCountMax=10 -o ExitOnForwardFailure=Yes -i /home/pi/.ssh/id_rsa_sftp_uqgec -N -R 1992:localhost:22 -C sftp@144.6.225.24
root      1821  0.2  1.5  11508  5724 ?        Ss   13:53   0:00 sshd: pi [priv]
pi        1830  0.1  1.0  11640  3968 ?        S    13:53   0:00 sshd: pi@pts/0
pi        1909  0.0  0.5   4364  2112 pts/0    S+   13:56   0:00 grep --color=auto ssh
```
Few updates:

1. -M 20000  should be changes for autossh as this is the way to do communications, as one can see this **-L 20001:127.0.0.1:20001 -R 20001:127.0.0.1:20002** 
2.  -o "ServerAliveCountMax=10" must be inplimented. as found during the weekend that if not, ssh from uqgec server will freeze (seems there are dead connections), while one can not get establish a reverse tunnel
3. i also reduced the number of forwarding port (removed 5901) as compiling arduino is doable from command line.
4. -o "ExitOnForwardFailure=Yes" is the right format (use equal rather than space)
5. it is also found that when i removed -o "ExitOnForwardFailure=Yes", and went for checking the system the next morning from the roof, the wifi thethering system also failed. 
6. we also had one command *echo howareyou? | netcat 127.0.0.1 20000* to send to port 20000 from the server, which could somehow interrupt the autossh.

```
2019/04/29 11:45:49 autossh[1026]: set alarm for 600 secs
2019/04/29 11:45:49 autossh[1028]: execing /usr/bin/ssh
2019/04/29 11:55:50 autossh[1026]: connection ok
2019/04/29 11:55:50 autossh[1026]: check on child 1028
2019/04/29 11:55:50 autossh[1026]: set alarm for 600 secs
2019/04/29 12:05:50 autossh[1026]: not what I sent: "stanwellmini autossh 1026 249585694 ^M
" : "howareyou?
"
2019/04/29 12:05:50 autossh[1026]: connection ok
2019/04/29 12:05:50 autossh[1026]: check on child 1028
2019/04/29 12:05:50 autossh[1026]: set alarm for 600 secs
2019/04/29 12:15:51 autossh[1026]: connection ok

```



