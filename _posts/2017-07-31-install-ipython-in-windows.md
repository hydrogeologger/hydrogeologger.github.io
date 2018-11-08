---
layout: post
title: install ipython in windows
---
solution: just install it in virtual machine
#1. disable internal wifi on boot 2017-06-15 10:35 
# Just put these to the file /etc/modprobe.d/raspi-blacklist.conf
#{% highlight bash %}
#blacklist brcmfmac
#blacklist brcmutil
#{% endhighlight %}
#
#2. use normal lan cable to connect laptop with rpi
#  This procedure is extremely important when using headless rpi as logger in the remote area.
#  For the rpi, one needs to append a small text in the file /boot/cmdline.txt:
#{% highlight bash %}
# ip=169.254.10.10
#{% endhighlight %}
#  Note that there is a space between the new string and existing strings. by doing this, one always gets same ip address at eth0:
#{% highlight bash %}
#pi@camellia:~ $ ifconfig
#eth0      Link encap:Ethernet  HWaddr b8:27:eb:83:c8:9d  
#          inet addr:169.254.10.10  Bcast:169.254.255.255  Mask:255.255.0.0
#          inet6 addr: fe80::ba27:ebff:fe83:c89d/64 Scope:Link
#          UP BROADCAST MULTICAST  MTU:1500  Metric:1
#          RX packets:70 errors:0 dropped:0 overruns:0 frame:0
#          TX packets:132 errors:0 dropped:0 overruns:0 carrier:0
#          collisions:0 txqueuelen:1000 
#          RX bytes:12403 (12.1 KiB)  TX bytes:22786 (22.2 KiB)
#{% endhighlight %}
#
#
#  For the laptop, one needs to do assign a static ip address as rpi has done. my laptop with Debian does not come up with file /boot/cmdline.txt and so I choose to change file /etc/network/interfaces
#
#{% highlight bash %}
#source /etc/network/interfaces.d/*
#{% endhighlight %}
#
## The loopback network interface
#{% highlight bash %}
#auto lo
#iface lo inet loopback
#
#
#auto eth2
#iface eth2 inet static
#    #your static IP
#    #address 192.168.1.118  
#    address 169.254.10.5
#    #your gateway IP
#    netmask 255.255.0.0
#    #your network address "family"
#    broadcast 169.254.255.255
#
#{% endhighlight %}
#
#now the system always get ip based on the static prescription.
#
#3. install anaconda
#4. the slash '/' in linux is equivalent to '\\' in windows
#
#
