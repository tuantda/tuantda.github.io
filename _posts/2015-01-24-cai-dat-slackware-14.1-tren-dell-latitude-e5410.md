---
layout: post
title: "Cài dat Slackware 14.1 tren Dell Latitude E5410"
published: true
tags: [linux, slackware]
categories: [blog]
---

### Cài đặt

#### Khởi động trình cài đặt


#### Phân vùng đĩa

Phân vùng ổ đĩa với 3 phân vùng '/', 'swap' và '/home'

    fdisk /dev/sda

#### Chọn kiểu cài đặt

Cài đặt **Full** Slackware theo hướng dẫn [Slackbook -
Install](http://www.slackbook.org/beta/#ch_install)

#### Post Install

Sau khi cài đặt xong, ta 'chroot' vào môi trường cài đặt để thay thế **huge**
với **generic** kernel.

Môi trường cài đặt được 'mount' tại '/mnt'

    mount --bind /dev /mnt/dev
    mount --bind /proc /mnt/proc
    mount --bind /sys /mnt/sys
    chroot /mnt

Cài đặt 'kernel-generic', 'kernel-module' và 'mkinitrd' từ thư mục
'slackware64/a' trong DVD cài đặt Slackware

    mount -t iso9660 /dev/sr0 /mnt/dvd
    cd /mnt/dvd/slackware64/a
    installpkg kernel-generic-$VERSION.txz
    installpkg kernel-module-$VERSION.txz
    installpkg mkinitrd-$VERSION.txz

Chuyển vào thư mục '/boot'

    cd /boot

Tiến hành tạo 'initrd' (initial ramdisk) theo filesystem là 'ext4' và phân vùng
root '/' nằm trên '/dev/sda3'

    mkinitrd -c -k 3.10.17-smp -m ext4 -f ext4 -r /dev/sda3

Tham khảo [Slackware initrd mini
HOWTO](http://mirrors.slackware.com/slackware/slackware-14.1/README.initrd)

Khởi động lại để hoàn tất cài đặt

    exit    #thoát môi trường chroot
    reboot

### Broadcom wireless

Dell Latitude E5410 đến với một Wireless card Broadcom BCM43224 không được hỗ
trợ trong driver 'b43' của kernel ([not
tested](http://wireless.kernel.org/en/users/Drivers/b43#Supported_devices). Ta
sẽ cài đặt driver 'wl' của Broadcom.

Đầu tiên, ta phải thêm tài khoản người dùng vào nhóm 'netdev'

    usermod -a -G netdev tài-khoản

Tạo gói cài đặt theo mã SlackBuild và mã nguồn 'broadcom-sta' từ
[SlackBuild.org](slackbuild.org) và cài đặt.

Thêm các driver sau vào '/etc/modprobe.d/blacklist.conf' để không xung đột với
driver 'wl' mới:

    blacklist ssb
    blacklist b43
    blacklist bcma

Khởi động lại máy hoặc nạp module on the fly

    rmmod ssb
    rmmod b43
    rmmod bcma
    modprobe wl

Để dễ quản lý các kết nối không dây, ta cài đặt 'wicd' trong thư mục 'extra'
của SlackwareDVD hoặc thông qua 'slackpkg' (với kết nối Internet thông qua cổng
Ethernet của máy)

    slackpkg install wicd

### Trackpad

Để sử dụng trackpad với các thiết đặt cuộn ngang, cuộn dọc, giả lập nút giữa
bằng cách nhấn hai nút trái, phải cùng lúc (dùng để paste từ clipboard), ta
chép `/usr/share/X11/xorg.conf.d/50-synaptics.conf` vào `/etc/X11/xorg.conf.d/`
và chỉnh sửa như sau:

    Section "InputClass"
    	Identifier "touchpad"
    	Driver "synaptics"
    	MatchDevicePath "/dev/input/event*"
    	MatchIsTouchpad "on"
    	Option "TapButton1" "1"
    	Option "TapButton2" "2"
    	Option "TapButton3" "3"
        #nút giữa thông qua nhấp 2 nút hoặc 2 ngón trên trackpad
    	Option "ClickFinger2" "3"
        #cuôn ngang và cuộn dọc
    	Option "VertEdgeScroll" "on"
    	Option "HorizEdgeScroll" "on"
    EndSection

Để  xem thêm thiết đặt, ta dùng lệnh `synclient`
