---
layout: post
title: "Cú pháp markdown"
published: true
tags: [markdown, cheatsheet]
---

Markdown là ngôn ngữ đánh dấu đơn giản, tạo thuận tiện cho việc chuyển đổi từ
văn bản thuần sang HTML. Đây là bản cú pháp markdown thần chưởng

* Bảng Nội Dung
{:toc}

## Tiêu đề (Header): {#header}

Một tiêu đề của đoạn văn được bắt đầu bằng _dấu thăng_ (`#`). Số lượng dấu thăng
thể hiện cấp độ của tiêu đề và không nhiều hơn sáu.

{% highlight text %}
# Tiêu đề 1
## Tiêu đề 2
### Tiêu đề 3 ###  (Dấu thăng # bên phải là tuỳ ý)
{% endhighlight %}

và khi tạo tiêu đề với ID như thế này:

{% highlight text %}
## Tiêu đề {#id}
{% endhighlight %}

sẽ tạo được liên kết đến tiêu đề đó:

{% highlight text %}
[Liên kết đến tiêu đề có ID](#id)
{% endhighlight %}

**Ghi chú:** _kramdown_ và _maruku_ hỗ trợ tạo bảng nội dung (table of content)
dựa trên các tiêu đề khi biên dịch sang HTML bằng cách thêm vào đoạn mã sau vào
đầu bài viết:
{: .notice}

{% highlight text %}
* Bảng nội dung
{:toc}
{% endhighlight %}

## Đoạn văn (Paragraph): {#paragraph}


Một đoạn văn bao gồm một dòng hoặc nhiều dòng.

Trong đoạn văn có thể có khoảng      trắng hoặc     tab. Các đoạn văn ngăn cách
nhau bằng một dòng trắng.

{% highlight text %}
Một đoạn văn bao gồm một dòng hoặc nhiều dòng.

Trong đoạn văn có thể có khoảng      trắng hoặc     tab. Các đoạn văn ngăn cách
nhau bằng một dòng trắng.
{% endhighlight %}

Đoạn văn có thể được xuống dòng bằng cách thêm _hai khoảng trắng_ hoặc
_hai dấu gạch chéo ngược_ (`\\`) vào cuối dòng như trong bài thơ sau:

{% highlight text %}
Quê hương là chùm kế ngọt\\
Cho con trèo hái mỗi ngày  
Quê hương là đường đi học\\
Con về rợp bóng cò bay.
{% endhighlight %}

## Đoạn trích dẫn (Blockquote) {#quote}

Đoạn trích dẫn được bắt đầu với _kí tự trích dẫn phải_ (`>`) tại đầu mỗi dòng
như khi trả lời email hay chỉ dòng đầu tiên  và có thể được lồng vào nhau.

{% highlight text %}
> đây là đoạn
trích dẫn.
>
> > được lồng vào nhau
thế này.
{% endhighlight %}

> đây là đoạn
trích dẫn.
>
> > được lồng vào nhau
thế này.

## Khối mã (Code block) {#code}

Các đoạn mã được trình bày bằng cách thêm _bốn khoảng trắng_ tại đầu mỗi
dòng mã (standard code block):

~~~
    Dòng mã 1
    Dòng mã 2
    Dòng mã 3
~~~

hoặc thêm các dấu ngã `~` (>=3) vào dòng trên và dòng dưới đoạn mã (fenced code
block):

{% highlight text %}
~~~
Dòng mã 1
Dòng mã 2
Dòng mã 3
~~~
{% endhighlight %}

Một đoạn mã với ngôn ngữ xác định:

{% highlight text %}
~~~ ruby
def what?
    42
end
~~~
{% endhighlight %}

{% highlight ruby %}
def what?
  42
end
{% endhighlight %}

**Ghi chú:** để định dạng mã trong câu văn (inline code), ta dùng dấu `` ` `` bao
quanh phần mã như thế này `` `inline code` ``
{: .notice}

## Đường kẻ ngang (Horizontal rule) {#hr}

Dùng ba dấu sao, dấu gạch ngang, dấu gạch chân viết liền hoặc cách nhau
khoảng trắng:

{% highlight text %}
***
* * *
---
- - -
___
_ _ _
{% endhighlight %}

***
* * *
---
- - -
___
_ _ _

## Danh sách (List) {#list}

{% highlight text %}
* Danh sách với kí tự sao
- Hoặc dấu trừ
+ Và dấu cộng
{% endhighlight %}

* Danh sách với kí tự sao
- Hoặc dấu trừ
+ Và dấu cộng

{% highlight text %}
1. Danh sách với số
2. Gồm số
3. Đi sau đó là dấu chấm và khoảng trắng
    1. Đây là
    2. danh sách con
69. Danh sách tự động đánh số tiếp theo
{% endhighlight %}

1. Danh sách với số
2. Gồm số
3. Đi sau đó là dấu chấm và khoảng trắng
    1. Đây là
    2. danh sách con
69. Danh sách tự động đánh số tiếp theo

## Danh sách định nghĩa (Definition list) {#definition}

{% highlight text %}
Rượu
: nho
: vang
{% endhighlight %}

Rượu
: nho
: vang

## Bảng (Table) {#table}

{% highlight text %}
| Header | Header | Right  |
|:-------|:------:|-------:|
|  Cell  |  Cell  |   $10  |
|  Cell  |  Cell  |   $20  |
| ====== | ====== | =====: |
| Footer | Footer | Footer |
{% endhighlight %}

| Header | Header | Right  |
|:-------|:------:|-------:|
|  Cell  |  Cell  |   $10  |
|  Cell  |  Cell  |   $20  |
| ====== | ====== | =====: |
| Footer | Footer | Footer |

+ Kí tự `|` bắt đầu một hàng
+ Kí tự `-` tách phần header của bảng
+ Kí tự `=` tách phần footer
+ Kí tự `:` gióng hàng trong cột (trái, phải hoặc 2 bên là gióng giữa)

## Nhấn mạnh chữ (Emphasis) {#emphasis}

{% highlight text %}
Đây là *chữ in nghiêng* và đây cũng _in nghiêng_

Đây là **chữ in đậm** và đây cũng __in đậm__
{% endhighlight %}

Đây là *chữ in nghiêng* và đây cũng _in nghiêng_

Đây là **chữ in đậm** và đây cũng __in đậm__

## Liên kết (Link) {#link}

Một *liên kết tự động* được tạo đơn giản với cặp móc nhọn (`<`,`>`) bao quanh
liên kết như thế này:

{% highlight text %}
<http://google.com>
{% endhighlight %}

<http://google.com>

hoặc cầu kỳ hơn với *liên kết nội tuyến*:

{% highlight text %}
Đây là trang [Google](http://google.com) và đây là trang [Google với tiêu
đề](http://google.com "Trang tìm kiếm Google")
{% endhighlight %}

Đây là trang [Google](http://google.com) và đây là trang [Google với tiêu
đề](http://google.com "Trang tìm kiếm Google")

Và đây là *liên kết tham chiếu*:
 
{% highlight text %}
Truy cập [trang tìm kiếm][Google] và đặt [Google] làm trang chủ

[Google]: http://google.com "google"
{% endhighlight %}

Truy cập [trang tìm kiếm][Google] và đặt [Google] làm trang chủ

[Google]: http://google.com "Trang tìm kiếm Google"

## Hình ảnh (Image) {#image}

Với hình ảnh cũng tương tự:

{% highlight text %}
![hoa](../images/hoa-anh-dao.jpg 'hoa anh đào')
{% endhighlight %}

![hoa](../images/hoa-anh-dao.jpg 'hoa anh đào')

## Lời chú cuối trang (Footnote) {#footnote}

{% highlight text %}
Đây là một ghi chú[^1]

[^1]: và đây là diễn giải footnote
{% endhighlight %}

Đây là một ghi chú[^1]

[^1]: và đây là diễn giải footnote

## Chữ viết tắt (Abbreviation) {#abbr}

{% highlight text %}
Đây là CVT

*[CVT]: Chữ Viết Tắt
{% endhighlight %}

Đây là CVT

*[CVT]: Chữ Viết Tắt

## Phần tử HTML (HTML) {#html}

Các cặp tag HTML cũng được hỗ trợ như thế này

{% highlight text %}
<div style="float: right">
Phần câu này trôi dạt sang bờ bên phải
</div>

Trong câu này, <span style="color: red">phần này được viết màu đỏ</span>, *phần
này màu xanh in nghiêng*{: style="color: blue"}
{% endhighlight %}

<div style="float: right">
Phần câu này trôi dạt sang bờ bên phải
</div>

Trong câu này, <span style="color: red">phần này được viết màu đỏ</span>, *phần
này màu xanh in nghiêng*{: style="color: blue"}
