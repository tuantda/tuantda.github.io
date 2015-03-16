---
layout: post
title: "Cài đặt gVim trên Windows 7"
published: true
tags: [windows, vim]
---

Vim là trình biên tập văn bản mạnh mẽ dựa trên Vi thường chạy trên các hệ thống
dựa trên UNIX. Bài viết này trình bày cách cài đặt gVim, một phiên bản đồ họa
(GUI) của Vim, trên Windows 7 và dùng Git, Pathogen để quản lý các phần bổ trợ
(plugin).

## Cài đặt gVim

Cài đặt gVim từ [trang chủ của Vim][vim]:

Chọn tùy chọn **Full** trong quá trình cài đặt:

{% include figure.html src="../images/vim_install_full.png" caption="Tùy chọn Cài đặt Full" %}

Mặc định, gVim sẽ cài vào đường dẫn `C:\Program Files (x86)`, chúng ta nên thay
đổi cài đặt vào thư mục nhà của người dùng `C:\Users\Tên_người_dùng` để dễ quản
lý cấu hình cùng các ứng dụng khác.

{% include figure.html src="../images/vim_install_path.png" caption="Chọn thư mục cài gVim" %}

## Quản lý plugin với Git và Pathogen

[Pathogen][pathogen] là một plugin quản lý `runtimepath`, giúp chúng ta dễ dàng
cài đặt các plugin và tệp runtime cho Vim vào một thư mục.

[Git][git] giúp chúng ta lưu trữ cấu hình của Vim để sử dụng lại trên nhiều
máy. Chúng ta dùng *Git Bash*  (cài đặt [Git for Windows][git4win]) để thực
hiện các lệnh bên dưới.

Trong thư mục cài đặt gVim mà ở đây là `%USSERPROFILE%\Vim`, chúng ta có các
thư mục sau nằm trong `runtimepath` (dùng lệnh `set runtimepath?` để xem):

    ~\Vim\vimfiles
    ~\Vim\vim74

Pathogen sẽ được đặt trong thư mục `autoload` để Vim tự nạp khi khởi chạy và
`pathogen` sẽ nạp các plugin được lưu trong thư mục `bundle`. Pathogen quản lý
tất cả nên chúng ta không cần những thứ rườm rà khác

    cd ~/vim                    # thư mục cài đặt Vim
    rm -rf vimfiles/*           # không cần những thứ rườm rà khác
    mv vim74/autoload vimfiles/ # Vim tự nạp plugin ở một nơi
    mkdir -p vimfiles/bundle    # thư mục chứa plugin
    git init                    # lưu trữ cấu hình vào git

Cài đặt pathogen

    curl -LSso vimfiles/autoload/pathogen https://tpo.pe/pathogen.vim

Thêm dòng sau đến tệp `_vimrc` để pathogen hoạt động

    execute pathogen#infect()

Cài đặt các plugin của Vim vào thư mục `bundle` như các `submodule` của Git

    git submodule add http://github.com/tpope/vim-fugitive.git vimfiles/bundle/fugitive
    git submodule add https://github.com/zeis/vim-kolor.git vimfiles/bundle/kolor
    git submodule init
    git submodule update
    git submodule foreach git submodule init
    git submodule foreach git submodule update

## Ghi chú:

### mswin.vim

map phím di chuyển lên, xuống, trái, phải vào j,k,h,l để dùng trong `Visual
Mode`

    if has("win32")
        map <down> j
        map <up> k
        map <right> l
        map <left> h
    endif

### Hiển thị tiếng Việt

Bảo gVim dùng mã hóa `UTF-8` không dùng mã hóa `CP-1252` của Windows

    set encoding=utf8

Chuyển ngôn ngữ thông báo sang tiếng Việt

    language message vi

Bảo gVim xóa menu hiện tại và dùng menu tiếng Việt chuẩn mã hóa `UTF-8`

    source $VIMRUNTIME/delmenu.vim
    set langmenu=vi_VN.UTF-8
    source $VIMRUNTIME/menu.vim
    
Đặt tất cả vào `_vimrc`

    set encoding=utf8
    if has("gui_running")
        language message vi
        source $VIMRUNTIME/delmenu.vim
        set langmenu=vi_VN.UTF-8
        source $VIMRUNTIME/menu.vim
    endif


[vim]: http://www.vim.org
[git]: http://git-scm.com
[pathogen]: https://github.com/tpope/vim-pathogen
[git4win]: {% post_url 2014-10-15-git-for-windows %}
