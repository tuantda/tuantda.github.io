---
layout: post
title: "Làm việc với Git"
published: true
tags: [git]
categories: blog
modified: 2013-12-11
---

Git là phần mềm quản lý mã nguồn phân tán được phát triển bởi Linus Torvalds
dành cho việc phát triển Linux kernel.

* Bảng Nội Dung
{:toc}

### Qui trình Git cơ bản {#workflow}

Dữ liệu trong repository được Git quản lý theo ba *tree*: **Working
Directory**, **Index (stage)** và **HEAD (commit)** [^1] theo qui trình sau:

<figure>
<img src="/images/git-workflow.png">
</figure>

### Các lệnh dùng trong qui trình {#command}

<figure>
<img src="/images/git-transport.png">
</figure>

Đây là một Git workflow đơn giản với các nguyên tắc cơ bản [^2]:

* Nhánh `master` phải luôn sẵn sàng được deploy
* **Chỉnh sửa, thay đổi** được thực hiện trên nhánh phụ/chức năng
* Dùng `rebase` để giải quyết xung đột trước khi `merge` vào nhánh `master`

{% highlight bash %}
# everything is happy and up-to-date in master
git checkout master
git pull origin master

# let's branch to make changes
git checkout -b my-new-feature

# go ahead, make changes now.
$EDITOR file

# commit your (incremental, atomic) changes
git add -p
git commit -m "my changes"

# keep abreast of other changes, to your feature branch or master.
# rebasing keeps our code working, merging easy, and history clean.
git fetch origin
git rebase origin/my-new-feature
git rebase origin/master

# optional: push your branch for discussion (pull-request)
#           you might do this many times as you develop.
git push origin my-new-feature

# optional: feel free to rebase within your feature branch at will.
#           ok to rebase after pushing if your team can handle it!
git rebase -i origin/master

# merge when done developing.
# --no-ff preserves feature history and easy full-feature reverts
# merge commits should not include changes; rebasing reconciles issues
# github takes care of this in a Pull-Request merge
git checkout master
git pull origin master
git merge --no-ff my-new-feature

# optional: tag important things, such as releases
git tag 1.0.0-RC1
{% endhighlight %}


[^1]: [Reset Demystified][git-scm-blog]
[^2]: [a simple git branching model][17twenty]

[git-scm-blog]: http://git-scm.com/blog/2011/07/11/reset.html
[17twenty]: https://gist.github.com/17twenty/6733076
