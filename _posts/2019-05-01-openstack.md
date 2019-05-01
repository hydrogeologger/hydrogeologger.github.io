---
layout: post
title: openstack 
---

I was bumped into learning openstack, the background engine for nectar cloud. the reason this is needed is that:

#### the server in the cloud needs to be backed up automatically, where web interface does not allow this to happen

#### the fixed ip address can not be preserved if the instances is crashed. 

#### openstack provides DNS, while DNS assissgnment could be done from commandline

## Installation
To learn this, i basically followed the webpage https://support.ehelp.edu.au/support/solutions/articles/6000075747-api

#### from dashboard -> API Access -> Download openstack RC file -> openstack RC file -> get file named a.rc
#### go to settings -> user settings -> reset pass word to get new password.
#### source a.rc, during which password will be required.


## useful commands

```
openstack server list # instances 
openstack flavor list 
openstack image list  #backuped images
openstack security group list 
```

I also assigned DNS to the system by the following command, based on this uqtailingsmonitoringengine.cloud.edu.au is been assigned to 203.101.226.97

```
openstack recordset create uqtailingsmonitoringengine.cloud.edu.au. --type A www --record 203.101.226.97
```


## making uqtailingsmonitoringengine.cloud.edu.au direct in connection to thingsboard with port 8080

thingsboard somehow can not be installed with default port as 80 (their default port is 8080),which makes web address ugly (e.g., www.uqgec.org:8080 ) so far the best way for me to remove the port is to impliment port forward from the server. for a debian 9, this is been done by:

```
iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
iptables-save > /etc/iptables/rules.v4
```

and in the file */etc/network/if-pre-up.d/iptables* put following script


```
#!/bin/sh
/sbin/iptables-restore < /etc/iptables.up.rules
```


so that iptables will be preserved at everytime system is rebooting.


