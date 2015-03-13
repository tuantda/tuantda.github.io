---
layout: post
title: "Cấu hình Slackware"
published: true
tags: [slackware]
---

## Post Install

Sau khi hoàn tất cài đặt và khởi động lại hệ thống, ta tiến hành một số tinh
chỉnh trước khi sử dụng hàng ngày.

### Thêm người dùng

Slackware cung cấp một đoạn mã giúp cho việc tạo thêm người dùng mới thật dễ
dàng. Gõ vào console dòng lệnh:

    adduser

và làm theo từng bước hướng dẫn rất chi tiết. Riêng phần nhóm tùy chọn ngoài
nhóm mặc định `users` mà người dùng thuộc về, ta chỉ nên dùng các nhóm mặc định
Slackware đã tạo sẵn (bằng cách nhấn mũi tên lên) vì chúng ta không muốn người
dùng thông thường can thiệp quá sâu vào hệ thống. Sau khi hoàn tất tạo người
dùng mới, chúng ta thoát khỏi `root` và đăng nhập vào người dùng vừa tạo.

### Cập nhật hệ thống

Chọn nột (**chỉ duy nhất 01**) mirror gần nhất bằng cách bỏ comment trong tệp
`/etc/slackpkg/mirrorsa`. Sau đó, tiến hành cập nhật hệ thống:

    slackpkg update gpg         # chỉ chạy 1 lần khi chọn/chuyển miror.
    slackpkg update             # cập nhật danh sách gói cài đặt
    slackpkg upgrade-all        # cập nhật các bản vá sửa lỗi (nếu có)

## Cấu hình X


## Thiết đặt font

Bật *autohint*, *subpixel* và *lcdfilter*

Dùng 
