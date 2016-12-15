---
layout: post
title: Slackware trên Dell Latitude E5410 - Cài đặt
published: true
tags:
  - linux
  - slackware
categories:
  - blog
---
*Update 12/12/2016:
- Chuyển từ Legacy/MBR sang UEFI/GPT
- Cài đặt Slackware với LUKS+LVM*

Slackware 14.2 đã được release. Lúc trước do có nhu dualboot Slackware với Windows 7 nên tui phải dùng Legacy/MBR cho đời đơn giản. Sau khi nâng RAM lên 8Gb, chuyển hướng các ứng dụng Windows sang máy ảo nên tui chuyển hẳn sang UEFI/GPT.

Boot Slackware-x64 DVD và tiến hành phân vùng ổ đĩa với 'gdisk'

    gdisk /dev/sda
    
Ở đây, chúng ta sẽ tạo 2 phân vùng:

- 1 phân vùng *EFI System* dung lượng khoảng 10Mb với mã là '0800'
- 1 phân vùng sẽ dùng cho toàn bộ *LVM* dung lượng là toàn bộ ổ đĩa còn lại với mã là '8e'

[Combining LUKS and LVM](http://ftp.slackware.com/pub/slackware/slackware-14.2/README_CRYPT.TXT)

#### Chọn kiểu cài đặt

Cài đặt **Full** Slackware theo hướng dẫn [Slackbook -
Install](http://www.slackbook.org/beta/#ch_install)

Sau khi cài đặt xong, ta 'chroot' vào môi trường cài đặt để thay thế **huge**
với **generic** kernel.

    chroot /mnt
    
Dùng script sau để tạo 'initrd', tích chọn vào các module cần thiết

    /usr/share/mkinitrd/mkinitrd_command_generator.sh -i > init
    chmod +x init
    ./init
    
Do phân vùng *EFI System* sẽ được mount vào '/boot/efi/EFI', ta chép 'initrd' và 'generic-kernel' vào thư mục này:

    cp -rfv /boot/initrd.gz /boot/efi/EFI/Slackware
    cp -rfv /boot/vmlinuz-generic-4.4.14 /boot/efi/EFI/Slackware
    
Chỉnh sửa '/boot/efi/EFI/Slackware/elilo.conf' để *elilo* biết sử dụng kernel 'generic':

    default=generic
    prompt
    chooser=simple
    timeout=60
    # huge
        label=huge
        image=vmlinuz
        initrd=initrd.gz
        append="resume=/dev/mapper-swap"
        read-only
        append="root=/dev/slack/root vga=normal ro"
        
    # generic
        label=generic
        image=vmlinuz-generic-4.4.14
        initrd=initrd.gz
        append="resume=/dev/mapper-swap"
        read-only
        append="root=/dev/slack/root vga=normal ro"

Tham khảo [Slackware initrd mini
HOWTO](http://mirrors.slackware.com/slackware/slackware-14.2/README.initrd)

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
[SlackBuilds.org](http://slackbuilds.org) và cài đặt.

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
