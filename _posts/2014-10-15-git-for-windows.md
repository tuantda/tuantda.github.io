---
layout: post
title: "Git for Windows"
published: true
tags: [git, windows]
---


Cài đặt Git trên Windows rất đơn giản. Dự án msysGit cung cấp một cách cài đặt
Git dễ dàng hơn. Đơn giản chỉ tải về tập tin cài đặt định dạng exe từ [trang
chủ Git][git4win],
và chạy

- Use `git-cheetah` plugin and TrueType Font

{% include figure.html src="../images/git_install_component.png" caption="use TrueType font" %}

- Git Bash only

{% include figure.html src="../images/git_install_env.png" caption="use Git from Git Bash" %}

- `core.autocrlf=input`

{% include figure.html src="../images/git_install_lineend.png" caption="set core.autocrlf=input" %}

- Attention: space in directory's name

{% include figure.html src="../images/git_install_path.png" caption="change default install directory" %}


[git4win]: http://git-scm.com/download/win
