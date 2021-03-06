---
layout: post
title: Mount disk image
---
## Create a directory for the disk that is to be mounted

Use the following to create a new directory and name it:

```bash
mkdir folder_name
```
E.g. osboxes@osboxes:~$mkdir hydrogeologgermount

Switch to root user
 
```bash
su
```
Then using following to list disk partitioning functions

```bash
fdisk -l /path/name.img
```
E.g root@osboxes:/home/osboxes# fdisk -l /media/sf_H_DRIVE/2018-05-30-pi3-hydrogeologger.img

More details see https://raspberrypi.stackexchange.com/questions/13137/how-can-i-mount-a-raspberry-pi-linux-distro-image

### Configuring a static IP

We are configuring a standalone network to act as a server, so the Raspberry Pi needs to have a static IP address assigned to the wireless port. This documentation assumes that we are using the standard 192.168.x.x IP addresses for our wireless network, so we will assign the server the IP address 192.168.4.1. It is also assumed that the wireless device being used is `wlan0`.

To configure the static IP address, edit the dhcpcd configuration file with: 
```bash
sudo vim /etc/dhcpcd.conf
```
Go to the end of the file and edit it so that it looks like the following:
```
interface wlan0
    static ip_address=192.168.4.1/24

```
Now restart the dhcpcd daemon and set up the new `wlan0` configuration:
```
sudo service dhcpcd restart

```

## Configuring the DHCP server (dnsmasq)

The DHCP service is provided by dnsmasq. By default, the configuration file contains a lot of information that is not needed, and it is easier to start from scratch. Rename this configuration file, and edit a new one:

```
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig  
sudo vim /etc/dnsmasq.conf
```

Type or copy the following information into the dnsmasq configuration file and save it:

```
interface=wlan0      # Use the require wireless interface - usually wlan0
  dhcp-range=192.168.4.2,192.168.4.20,255.255.255.0,24h
```

So for `wlan0`, we are going to provide IP addresses between 192.168.4.2 and 192.168.4.20, with a lease time of 24 hours. If you are providing DHCP services for other network devices (e.g. eth0), you could add more sections with the appropriate interface header, with the range of addresses you intend to provide to that interface.

There are many more options for dnsmasq; see the [dnsmasq documentation](http://www.thekelleys.org.uk/dnsmasq/doc.html) for more details.

## Configuring the access point host software (hostapd)

You need to edit the hostapd configuration file, located at */etc/hostapd/hostapd.conf*, to add the various parameters for your wireless network. After initial install, this will be a new/empty file.

```bash
sudo vim /etc/hostapd/hostapd.conf
```

Add the information below to the configuration file. This configuration assumes we are using channel 7, with a network name of NameOfNetwork, and a password AardvarkBadgerHedgehog. Note that the name and password should **not** have quotes around them. The passphrase should be between 8 and 64 characters in length.

```bash
interface=wlan0
driver=nl80211
ssid=NameOfNetwork
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=AardvarkBadgerHedgehog
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

We now need to tell the system where to find this configuration file.

```bash
sudo vim /etc/default/hostapd
```

Find the line with #DAEMON_CONF, and replace it with this:

```bash
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```

## Start it up

Now start up the remaining services:

```bash
sudo systemctl start hostapd
sudo systemctl start dnsmasq
```
### Add routing and masquerade

Edit **/etc/sysctl.conf** and uncomment this line:
```
net.ipv4.ip_forward=1
```

Add a masquerade for outbound traffic on eth0 (outbound **eth0** here mean a network that are permanently connected to internet):
```
sudo iptables -t nat -A  POSTROUTING -o eth0 -j MASQUERADE
```
Save the iptables rule.
```
sudo sh -c "iptables-save > /etc/iptables.ipv4.nat"
```

Edit **/etc/rc.local** and add this just above "exit 0" to install these rules on boot.
```
iptables-restore < /etc/iptables.ipv4.nat
```
Reboot

Using a wireless device, search for networks. The network SSID you specified in the hostapd configuration should now be present, and it should be accessible with the specified password.

If SSH is enabled on the Raspberry Pi access point, it should be possible to connect to it from another Linux box (or a system with SSH connectivity present) as follows, assuming the `pi` account is present:

```
ssh pi@192.168.4.1
```

By this point, the Raspberry Pi is acting as an access point, and other devices can associate with it. Associated devices can access the Raspberry Pi access point via its IP address for operations such as `rsync`, `scp`, or `ssh`.

## ----------------------------------------------------------------------------------
<a name="internet-sharing"></a>
## Using the Raspberry Pi as an access point to share an internet connection (bridge) NOT NECESSARY

One common use of the Raspberry Pi as an access point is to provide wireless connections to a wired Ethernet connection, so that anyone logged into the access point can access the internet, providing of course that the wired Ethernet on the Pi can connect to the internet via some sort of router.

To do this, a 'bridge' needs to put in place between the wireless device and the Ethernet device on the access point Raspberry Pi. This bridge will pass all traffic between the two interfaces. Install the following packages to enable the access point setup and bridging.

```
sudo apt-get install hostapd bridge-utils
```

Since the configuration files are not ready yet, turn the new software off as follows: 

```
sudo systemctl stop hostapd
```
Bridging creates a higher-level construct over the two ports being bridged. It is the bridge that is the network device, so we need to stop the `eth0` and `wlan0` ports being allocated IP addresses by the DHCP client on the Raspberry Pi.

```
sudo vim /etc/dhcpcd.conf
```

Add `denyinterfaces wlan0` and `denyinterfaces eth0` to the end of the file (but above any other added `interface` lines) and save the file.

Add a new bridge, which in this case is called `br0`.

```
sudo brctl addbr br0
```

Connect the network ports. In this case, connect `eth0` to the bridge `br0`.

```
sudo brctl addif br0 eth0
```

Now the interfaces file needs to be edited to adjust the various devices to work with bridging. `sudo vim /etc/network/interfaces` make the following edits.

Add the bridging information at the end of the file.

```
# Bridge setup
auto br0
iface br0 inet manual
bridge_ports eth0 wlan0

```    

The access point setup is almost the same as that shown in the previous section. Follow the instructions above to set up the `hostapd.conf` file, but add `bridge=br0` below the `interface=wlan0` line, and remove or comment out the driver line. The passphrase must be between 8 and 64 characters long. 

```
interface=wlan0
bridge=br0
#driver=nl80211
ssid=hydrogeologger
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=123123123
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

Now reboot the Raspberry Pi.

There should now be a functioning bridge between the wireless LAN and the Ethernet connection on the Raspberry Pi, and any device associated with the Raspberry Pi access point will act as if it is connected to the access point's wired Ethernet.

The `ifconfig` command will show the bridge, which will have been allocated an IP address via the wired Ethernet's DHCP server. The `wlan0` and `eth0` no longer have IP addresses, as they are now controlled by the bridge. It is possible to use a static IP address for the bridge if required, but generally, if the Raspberry Pi access point is connected to a ADSL router, the DHCP address will be fine.

## ----------------------------------------------------------------------------------
<a name="enquiry"></a>



/var/lib/misc/dnsmasq.leases 

get all the ip addresses that has been released


reference:

https://superuser.com/questions/1238698/get-all-the-ip-addresses-given-out-by-dhcp-server-with-dnsmasq-and-hostapd
