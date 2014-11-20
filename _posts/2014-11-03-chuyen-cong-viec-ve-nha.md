---
layout: post
title: "Chuyển công việc dang dở về nhà với Git"
published: true
tags: [git]
---

Nhu cầu là tui cần chuyển các công việc dang dở ở công ty về nhà làm tiếp nhưng
lại không muốn public những thay đổi này.

Quy tắc là nhánh `master` luôn sạch vì vậy các công việc của chúng ta luôn diễn
ra ở nhánh chức năng.

- Tại công ty, tạo một *commit* tạm thời chứa tất cả những công việc dang dở muốn
  đem về nhà trong nhánh `chuaxong` và `push` lên *remote* `work`

        git commit -m "[uncompleted]VỀ NHÀ LÀM TIẾP"
        git push work chuaxong

- Khi về nhà, chúng ta `pull` từ *remote* `work` xuống máy nhà

        git pull work chuaxong

- Kế đến, chúng ta xóa *commit* tạm thời tại *remote* mà chúng ta đã `push` lên
  tại công ty. 
  
  **Chú ý:** *commit* tạm thời là *commit* cuối cùng (`HEAD`) tại
  *remote*, vì vậy, chúng ta bảo *remote* chuyển sang cha của *commit* cuối
  (`HEAD^`) với một *non-fastforward push* (`+`)

        git push work +HEAD^:chuaxong

- Bây giờ việc đơn giản chỉ là xóa *commit* tại nhà và tiếp tục công việc

        git reset HEAD^

Việc này chỉ nên tiến hành trên một *remote* riêng, đối với *share remote*, nên
sử dụng lệnh `git revert`
