---
layout: post
title: "Kiểm tra chính tả tiếng Việt trong Vim"
published: true
tags: [vim, spell, vietnamese]
description: "cách thức kiểm tra tiếng Việt trong Vim 7"
---


Từ phiên bản 7, tính năng kiểm tra chính tả (spellcheck) đã được tích hợp sẵn.
Mặc định, Vim chỉ kiểm tra tiếng Anh. Để kiểm tra ngôn ngữ khác, Vim hỗ trợ tạo
các tập tin chính tả theo định dạng Vim từ các gói Aspell/Hunspell thông qua
lệnh `mkspell` trong Vim.

## Kiểm tra chính tả spellcheck

### Tạo tập tin kiểm tra chính tả theo định dạng Vim

Trang dự án [Bộ kiểm tra chính tả tiếng Việt][vi-hunspell] cung cấp các gói
kiểm tra chính tả dùng cho OpenOffice/LibreOffice, Firefox/Thunderbird và
Hunspell. Để tạo bộ kiểm tra chính tả cho tiếng Việt, chúng ta tải về gói
Hunspell `vi_VN.zip`.

Tiến hành giải nén:

{% highlight bash %}
unzip vi_VN.zip -d vi-spell
Archive:  vi_VN.zip
inflating: vi-spell/vi_VN.dic
inflating: vi-spell/vi_VN.aff
{% endhighlight %}

Mở Vim với mã kí tự (*encoding*) muốn dùng tại thư mục vừa giải nén và tiến hành
biên dịch từ điển.

Trên hệ thống kiểu Unix:

{% highlight bash %}
export LANG=vi_VN.UTF-8 vim
:mkspell vi vi_VN
{% endhighlight %}

trong đó `vi` là tên ngôn ngữ của từ điển sẽ biên dịch, `vi_VN` là tên tập tin
đã giải nén không kèm theo đuôi `.aff` và `.dic` (ở đây là `vi_VN.aff` và
`vi_VN.dic`). Vim sẽ dựa trên mã kí tự và biên dịch ra một tập tin trong
trường hợp này là `vi.utf-8.spl`. Sao chép tập tin này vào thư mục
`$VIMRUNTIMEPATH/spell` để sử dụng.

### Sử dụng

Để bắt đầu sử dụng tập tin kiểm tra chính tả vừa tạo, ta bật chức năng kiểm tra
chính ta bằng lệnh:

{% highlight vim %}
:set spell spelllang=vi
{% endhighlight %}

hoặc kiểm tra chính tả cả Anh và Việt:

{% highlight vim %}
:set spell spelllang=en,vi
{% endhighlight %}

Sau khi bật, Vim sẽ gạch dưới (hoặc tô sáng nếu trong terminal) các từ sai bằng
màu đỏ, các từ hiếm bằng màu cam, các từ không viết hoa đầu dòng bằng màu xanh
dương,...

### Các lệnh cần nhớ

+ **]s** : di chuyển đến từ kế tiếp
+ **[s** : di chuyển đến từ trước
+ **zg** : thêm từ vào từ điển
+ **zug** : xóa từ vừa thêm khỏi từ điển
+ **z=** : xem từ đề nghị cho từ sai

## Tự động chỉnh sửa từ sai

Dùng chức năng viết tắt của Vim để tự chỉnh sửa từ viết sai theo thói quen.


{% highlight bash %}
:ab hoàgn hoàng
{% endhighlight %}

Khi bạn gõ `hoàgn` sẽ được thay thế với `hoàng`

Chức năng này rất giống macro của Unikey, vì vậy chúng ta có thể tạo các từ
viết tắt để Vim tự thay thế cho nhanh

{% highlight vim %}
:ab m@il tui@mail.net
{% endhighlight %}

[vi-hunspell]: https://code.google.com/p/hunspell-spellcheck-vi/
