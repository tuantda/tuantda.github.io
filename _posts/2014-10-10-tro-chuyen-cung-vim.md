---
layout: post
title: "Trò chuyện cùng Vim"
published: true
tags: [vim]
---


Vim có một bộ các từ mô tả các *verb (hành động)*, *modifier (bổ nghĩa)* và
*object (đối tượng)* rất dễ nhớ. Khi kết hợp các từ này với nhau, ta sẽ tận
dụng được sức mạnh của Vim để giảm thiểu những công việc nhàm chán lặp đi lặp
lại hàng ngày. Điều đặc biệt là việc kết hợp này sẽ trở thành các câu trò
chuyện thú vị giữa chúng ta và Vim với cấu trúc ngữ pháp sau:

{% highlight text %}
hành động - bổ nghĩa - đối tượng
{% endhighlight %}

Đây là một số bộ từ của Vim:

{% highlight text %}
verb     : visual, change, delete, yank, repalce
modifier : inside, around, till, find, /
object   : word, sentence, paragraph, block
{% endhighlight %}

Bây giờ, hãy tưởng tượng bạn đang làm việc cùng cô trợ lý xinh đẹp và tài năng
Vim. Thay vì chúng ta cầm tay chỉ việc, nghĩa là nhấn phím này, phím kia lặp đi
lặp lại thì hãy nói ra ý muốn của mình để cô trợ lý tài năng xử lý cho chúng
ta.

Một ví dụ đơn giản, để xóa một câu trong một đoạn, chúng ta sẽ làm gì? Nhấn `v`
để chọn, dùng phím trái, phải để chọn toàn bộ câu và nhấn `d` để xóa. Bây giờ
chúng ta chỉ đơn giản bảo "hãy xóa toàn bộ câu" (`d`elete `a`round `s`entence):

{% highlight vim %}
das
{% endhighlight %}

Một ví dụ khác, để sửa đổi câu "hãy xóa toàn bộ câu", ta hãy bảo Vim "sửa đổi
bên trong dấu `"`" (`c`hange `i`nside `"`) và nhập thông tin sửa đổi.

{% highlight vim %}
ci"
{% endhighlight %}

và `vap` để chọn toàn đoạn trên thay vì dùng `V` và phím lên, xuống để chọn.

Để tạo một dòng 72 kí tự `"` thế này trong `vimrc`:

{% highlight vim %}
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
{% endhighlight %}

ta nhấn `i` và lặp đi lặp lại nhập kí tự `"` 72 lần hay chỉ đơn giản bảo Vim
"nhập kí tự `"` 72 lần" như thế này:

{% highlight vim %}
79i"<Esc>
{% endhighlight %}

Dài dòng hơn nữa, ta sẽ bảo Vim tạo header trong markdown thế này

{% highlight bash %}
Trò chuyện cùng Vim
===================
{% endhighlight %}

Việc đầu tiên, chúng ta gõ:

{% highlight bash %}
Trò chuyện cùng Vim
{% endhighlight %}

và bảo Vim `Y`ank (copy) dòng trên, `p`aste (dán) xuống dưới, `V`isual (chọn)
dòng dưới này và `r`eplace (thay thế) với dấu `=`:

{% highlight vim %}
YpVr=
{% endhighlight %}

Xin vui lòng đọc tài liệu `:help motion.txt` để hiểu rõ hơn.
