---
layout: post
title: "Mẹo dùng Vim"
published: true
tags: [vim, tips]
description: "Các mẹo về tìm kiếm, thay thế, di chuyển trong Vim"
---

Vim là *elvis* trong Slack và cũng là dụng cụ vận động ngón tay ưa thích của
tui. Note lại mấy cái bài tập đánh vần để sau này già khỏi quên.

* Bảng nội dung
{:toc}

## Di chuyển trong Vim (Normal Mode) {#moving}

{% highlight text %}
             lên (k)
trái (h)                phải (l)
             xuống (j)

0            : về đầu dòng
$            : đến cuối dòng
}            : nhảy đến 1 đoạn
{            : nhảy lui 1 đoạn
gg (hoặc 1G) : về đầu tệp
G            : đến cuối tệp
50G          : đến dòng 50
%            : di chuyển đến ngoặc đóng của ngoặc mở tương ứng
{% endhighlight %}

### Hiện trạng thái tệp {#status}

+ `:=`     : hiện tổng số dòng của tệp
+ `ctrl+G` : hiện tên, số dòng, tổng số dòng và số % vị trí hiện tại của tệp

## Chọn Text {#select}

Trong **Normal Mode**, dùng các lệnh sau để chọn text, các phần text được chọn
sẽ được tô sáng.

{% highlight text %}
v                             : chọn khoảng text
V                             : chọn toàn bộ hàng
ctrl+v (ctrl+q trên Windows)  : chọn cột
gv                            : chọn lại khối vừa chọn
ggVG                          : chọn toàn bộ tệp
vap (visual around paragraph) : chọn đoạn này
{% endhighlight %}

Sau khi chọn text, chúng ta có thể cắt, copy (`d`, `y`), định dạng (`:center`,
`:left`, `:right`), sort (`:!sort`), tìm thay thế (`:s/khớp/thay/`), ...

## Tìm kiếm {#searching}

- Các biến nên thiết đặt:

{% highlight text %}
:set ignorecase - không phân biệt hoa thường
:set smartcase  - tìm chữ hoa khi chữ hoa được gõ
:set incsearch  - hiển thị kết quả khi gõ từ tìm kiếm
:set hlsearch   - tô sáng kết quả
{% endhighlight %}

- Các lệnh tìm kiếm cơ bản:

{% highlight text %}
/từ-cần-tìm   - tìm tiếp từ cần tìm
n             - lặp lại quá trình tìm tiếp
*             - tìm chính xác từ dưới trỏ (rain không tìm rainbow)
g*            - tìm tất cả từ chứa từ dưới trỏ (khác *)
{% endhighlight %}


## Tìm và thay thế {#replace}

{% highlight text %}
:[range]s/cần-tìm/thay-thế/flags
{% endhighlight %}

- `range` : gồm `%` cho toàn bộ tệp hoặc `từ-dòng,đến-dòng` chọn trong *Visual*
- `flags` : gồm `g` thay toàn bộ; `c` xác nhận và `i` phân biệt hoa thường

### Mẹo: dùng tìm kiếm để thêm, xóa kí tự

- Tìm từ `foo` và xóa với xác nhận

{% highlight text %}
:%s/foo//gc
{% endhighlight %}

- Thêm, xóa kí tự tại đầu hoặc cuối dòng

{% highlight text %}
:[range]s/^/foo      # Thêm foo tại đầu dòng
:[range]s/$/foo      # Thêm foo tại cuối dòng
:[range]s/^..//      # Xóa 2 ký tự tại đầu dòng
:[range]s/..$//      # Xóa 2 ký tự tại cuối dòng
{% endhighlight %}

  **Ghi chú:** `.` *(dấu chấm)* đại diện cho một ký tự (một *khoảng trắng* hoặc
  một *tab* cũng là một ký tự).

- Thêm một vài khoảng trắng đầu dòng (hữu ích khi định dạng đoạn mã)

{% highlight text %}
:[range]s/^/    /    # thêm 4 khoảng trắng đầu dòng
{% endhighlight %}

- Xóa các khoảng trắng không muốn cuối dòng

`\s` sẽ tìm khoảng trắng, `\+` tìm theo số lần xuất hiện

{% highlight text %}
:%s/\s\+$//
{% endhighlight %}


## Một số biến tùy chỉnh

### Tùy chỉnh kích cỡ cửa sổ

{% highlight text %}
set lines=29   : hiển thị 30 hàng
set columns=90 : hiển thị 90 cột
{% endhighlight %}

[Trò chuyện với Vim]: {% post_url 2014-10-10-tro-chuyen-cung-vim %}
