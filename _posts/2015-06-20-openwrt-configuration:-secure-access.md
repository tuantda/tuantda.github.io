---
layout: post
title: "OpenWRT Configuration: Secure Access"
published: true
tags: [openwrt]
categories: [blog]
---


We only connect to OpenWRT router over SSH using public key authencation. LuCI web interface is disabled and is accessed over SSH.

## Setup SSH access

We copy *public key* to router using `scp`

	scp ~/.ssh/id_rsa.pub root@192.168.1.1:/tmp
	
We connect to router using SSH with password and tell *dropbear* use our public key for authencation

	cat /tmp/id_rsa.pub >> /etc/dropbear/authorized_keys
	
Next, let's setup dropbear not to listen default port 22 and disable all users login with password.

Edit file `/etc/config/dropbear`

	config dropbear
		option Port '2222' 				# use port 2222
		option RootPasswordAuth 'off' 	# disable root login with password
		option PasswordAuth 'off'		# disable login with password
		
## Secure LuCI web interface

We disable LuCI and start service via SSH when needed

	/etc/init.d/uhttpd disable
	/etc/init.d/uhttpd stop
	
When we need access LuCI, we start `uhttpd` service from SSH and access it via SSH tunnel

	ssh -L127.0.0.1:8000:127.0.0.1:80 root@openwrt.lan
	/etc/init.d/uhttpd start
	
Open browser and connect to address `127.0.0.1:8000` to access LuCI