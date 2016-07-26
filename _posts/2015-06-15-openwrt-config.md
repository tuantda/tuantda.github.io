---
layout: post
title: "OpenWRT Basic Setup"
published: true
tags: [openwrt]
---


## First Login ##

### Telnet ###

Default, *dropbear* (SSH service) doesn't accept any connections at firstlogin, we can use *telnet* to
connect to router via default IP address:

    telnet 192.168.1.1
    passwd
    exit

After we set a password for OpenWRT, *telnet* deamon will be disabled. We can
login again with *ssh* `ssh root@192.168.1.1`

### LuCI ###

Open your browser and connect to the router at its default address (usually
*192.168.1.1*). Login using username *root* with an empty password.

Then click on the menu in the top bar on *Administration -> System*. A page to
change the password is displayed.

## Network ##

Network configuration is located in the file */etc/config/network*. We can
determine the configurations including *VLAN, interfaces, routing* in this
file.

After editing, we need to excute the following command

    /etc/init.d/network reload

to reload the network without reboot router.

### Internet Connection ###

We connect to Internet via a device (bridged function) over Ethernet cable,
means we log in to the ISP through a  DSL modem or fiber converter has been set
up. In this case, we use PPPOE to connect to the Internet.

Install packages for PPPOE connecting

    opkg update
    opkg install ppp kmod-pppoe ppp-mod-pppoe

We can edit manually or use *UCI command line* to config connection information

    uci set network.wan.proto=pppoe
    uci set network.wan.username='username_from_isp'
    uci set network.wan.password='password'
    uci commit network

Check file */etc/init.d/network* if it has following section:

    config 'interface' 'wan'
    	option 'proto'		'pppoe'
		option 'username'	'username_from_isp'
		option 'password'	'password'

then reload network.

### Wireless Config ###



### Access DSL modem ###


