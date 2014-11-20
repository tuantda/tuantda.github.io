---
layout: post
title: "Sử dụng tính năng hoàn tất từ, dòng trong soạn thảo"
published: true
tags: [latex, vim]
---


Cô trợ lý xinh đẹp đáng yêu Vim với kỹ năng `completion` đã hỗ trợ tui rất tốt
trong quá trình soạn thảo tùm lum tùm la, đặc biệt là với LaTex, Python.

### Hoàn tất theo các từ, dòng tương tự trong tệp hiện tại

Trong chế độ `Insert`, gõ vài chữ đầu và nhấn các phím tắt sau:

`ctrl-n`/`ctrl-p` : hoàn tất từ tương tự đã gõ trong tệp (next/previous)

`ctrl-x` `ctrl-l` : hoàn tất dòng tương tự đã gõ (chọn với `ctrl-n`, `ctrl-p`)

### Hoàn tất theo tệp từ điển

Trong quá trình sử dụng LaTex, do lo ngại vấn đề chính tả khi gõ lệnh LaTex,
tui muốn Vim hỗ trợ tui hoàn tất các lệnh này từ một tệp lệnh LaTex đã biết.

Đầu tiên, chúng ta phải tạo/sao chép một tệp từ điển lệnh LaTex với cấu trúc
mỗi hàng một lệnh. Tui chép ngay từ bộ plugin [Vim LaTex][latex-suite] cho
nhanh việc và đưa luôn vào thư mục `spell` của Vim (với Python, có thể chép từ
plugin [pydiction][pydiction]).

Bảo với Vim sử dụng tệp từ điển này (gVim trên Windows):

{% highlight vim %}
set dictionary+=~/Vim/vim74/spell/latex-commands
{% endhighlight %}

Chúng ta có thể thêm, xóa tệp từ điển bằng các lệnh `dictionary+`,
`dictionary-`. Sử dụng lệnh `set dictionary?` để xem Vim đang dùng tệp từ điển
nào.

Bây giờ chúng ta có thể bảo Vim hoàn tất lệnh từ tệp từ điển này trong chế độ
`Insert` bằng các phím tắt `ctrl-x ctrl-k` và dùng `ctrl-n` hoặc `ctrl-p` để
chọn từ cần hoàn tất.

Ví dụ để hoàn tất lệnh `\documentclass`:

{% highlight vim %}
\do<ctrl-x><ctrl-k><ctrl-n>
{% endhighlight %}

[latex-suite]: http://vim-latex.sourceforge.net/
[pydiction]: https://github.com/rkulla/pydiction
