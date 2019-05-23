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
openstack project list
openstack server list # instances 
openstack flavor list 
openstack image list  #backuped images
openstack image list --name thingsboard-just-setup-190430
openstack image show myCirrosImage
openstack security group list 
openstack recordset list  uqtailingsmonitoringengine.xx.xxx.xx. # list all dns service.
openstack image member list hydrogeologger190507


```


```
nova list  # list all the running instances
```

I also assigned DNS to the system by the following command, based on this uqtailingsmonitoringengine.cloud.edu.au is been assigned to 203.101.226.97

```
openstack recordset create uqtailingsmonitoringengine.cloud.edu.au. --type A www --record 203.101.226.97
```

below command is able to make a CNAME:

```
openstack recordset create uqtailingsmonitoringengine.cloud.edu.au.  uqgec2 --type CNAME  --record www.uqtailingsmonitoringengine.cloud.edu.au.
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


## backup instances:
following webpage https://docs.openstack.org/ocata/user-guide/cli-use-snapshots-to-migrate-instances.html


```
#openstack server image create  --name myInstanceSnapshot
nova image-create --poll hydrogeologger hydrogeologger190507
```

below script save image to a local file (this may not be necessary as the file can be safely stored in the cloud)

```
openstack image save --file 190430_uqgec_snapshot 8be923ef-01af-4585-b9f8-c38715913248
```

https://docs.openstack.org/mitaka/user-guide/cli_use_snapshots_to_migrate_instances.html

below save the instance to a image online
```
nova image-create --poll hydrogeologger hydrogeologger190507
nova image-list
glance image-download --file  hydrogeologger190507 2de20fd4-74ac-4876-96bd-71852edd54b0  # save the file to another machine

# give one image to another project https://ask.openstack.org/en/question/4653/openstack-glance-how-to-share-image/
#glance member-create <image-uuid> <project-uuid>
# it is found that when the image is creat

glance member-create 2de20fd4-74ac-4876-96bd-71852edd54b0 562bdbc46e6b4ea99490e7a92d32c652


# change image to shared images, one could refer the image name or id. 
openstack image set --shared 2de20fd4-74ac-4876-96bd-71852edd54b0
openstack image set --shared hydrogeologger190507

# check if a member is able to go to a site. using a name to referr to a image would be better than id. 
openstack image member list  thingsboard-just-setup-190430


```

