---
layout: post
title: "Lỗi piix4_smbus trên Virtualbox"
published: true
tags: [virtualbox]
---

Khi khởi động máy ảo Linux trên Virtualbox xuất hiện dòng thông báo lỗi
sau (không ảnh hưởng đến hệ thống):

{% highlight bash %}
piix4_smbus 0000.00.07.0: SMBus base address uninitialized - upgrade bios or use force_addr=0xaddr
{% endhighlight %}

Các bước sau sẽ loại bỏ dòng thông báo khó chịu này:

- Kiểm tra xem module sau có được nạp bằng lệnh: 
    {% highlight bash %}
    lsmod | grep i2c_piix4
    {% endhighlight %}
- Không nạp module này lúc khởi động: 
    {% highlight bash %}
    echo 'blacklist i2c_piix4' >> /etc/modprobe.d/blacklist.conf
    {% endhighlight %}
- Cập nhật `initramfs` với lệnh:
    {% highlight bash %}
    update-initramfs -u -k all
    {% endhighlight %}
