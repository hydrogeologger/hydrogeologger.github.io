---
layout: post
title: sftp uqgec localhost port number for pi and pizero devices
---

1. hydrogeologgermini (currently working on the roof for the stanwell project)
```bash
   ssh pi@localhost -p 1992
```
Telstra 3g usb modem is used to provide internet
Pi zero is working as wifi router to provide internet for photon weather station
   

2. hydrogeologger (the pi 3 B+ sitting on chenming's desk)
```bash
   ssh pi@localhost -p 1993
```
the pi 3 B+ connect to uq wifi
the pi is working as wifi router

3. hydrogeologgermini (deployed in gelita)

```bash
   ssh pi@localhost -p 20007
```

Telstra 3g usb modem is used to provide internet
Pi zero is working as wifi router

4. hydrogeologgermini (deployed in gelita) 

```bash
   ssh pi@localhost -p 20003
```
Autossh is setup in Ximing's mango
Telstra 3g usb modem is used to provide internet
Pi zero is working as wifi router to provide internet to photon weather station

5.number of ports required by each autossh

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
