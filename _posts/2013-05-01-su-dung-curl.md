---
layout: post
title: "Sử dụng cURL"
published: true
tags: [curl]
categories: blog
description: "Sử dụng cURL tải một hay nhiều tập tin cùng lúc; tải toàn bộ trang
web"
---

cURL là ứng dụng dòng lệnh dùng truyền dữ liệu theo URL cho trước. So với wget
thì cá nhân tui thích cURL hơn do những điều khó nói mà chỉ có đọc manual mới
nói được.

### Tải nhiều tập tin theo liên kết cho trước

Ví dụ tôi cần tải các ảnh truyện của chap 883 Thám tử Conan từ liên kết này:
[http://data.kenhsinhvien.net/conan/vol83/chap883/KSV_Rocketeam_830801.jpg](http://data.kenhsinhvien.net/conan/vol83/chap883/KSV_Rocketeam_830801.jpg)

{% highlight bash %}
chap=Chap883
pic=http://data.kenhsinhvien.net/conan/vol83/chap883/KSV_Rocketeam_8308[01-16].jpg
curl $pic -o $chap_#1.jpg
{% endhighlight %}

- `[01-16]`: tải từ ảnh 01 đến ảnh 16
- `#1`: biến thiên từ 01 đến 16
