---
layout: post
title: "Vim plugin"
published: true
tags: [vim]
---

## [Pathogen](https://github.com/tpope/vim-pathogen)

Plugin quản lý `$VIMRUNTIME`

    execute pathogen#infect()
    execute pathogen#helptags()

## [Vim-Gitgutter](https://github.com/airblade/vim-gitgutter)

Hiển thị `git diff` của tệp với lần `commit` cuối nơi cột trái của cửa sổ gVim.

## [Fugitive](https://github.com/tpope/vim-fugitive)

Quản lý Git trong Vim

`Gstatus`

## [Syntastic](https://github.com/scrooloose/syntastic)

Kiểm tra cú pháp mã nguồn các ngôn ngữ lập trình

## [Trailing-Whitespace](https://github.com/bronson/vim-trailing-whitespace)

Hiển thị các khoảng trắng cuối dòng bằng màu đỏ.

Để xóa các khoảng trắng thừa đó, dùng lệnh:

    :FixWhitespace

## [SuperTab](https://github.com/ervandew/supertab)

tab completetion

## [AutoClose](https://github.com/Townk/vim-autoclose)

Tự động chèn kí tự đóng

    <Leader>a

## [Tabular](https://github.com/godlygeek/tabular)

Gióng hàng theo kí tự

    :Tabularize /,/r1c1l0

            Some short phrase , some other phrase
    A much longer phrase here , and another long phrase

## [Easy-Align](https://github.com/junegunn/vim-easy-align)

Tiện ích gióng hàng đơn giản và tiện lợi

apple   =red
grass+=green
sky-=   blue

Chọn đoạn trên với lệnh `vip`, nhấn `Enter` để dùng lệnh, nhấn `=` để gióng
đoạn theo dấu `=` hoặc nhấn `Enter` để chọn kiểu gióng (`R`ight, `C`enter) và
nhấn `Space` để gióng hàng
