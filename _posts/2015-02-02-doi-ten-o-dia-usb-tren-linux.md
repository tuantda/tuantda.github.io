---
layout: post
title: "Đổi tên ổ đĩa USB trên Linux"
published: true
tags: [linux]
---

Kiểm tra các ổ đĩa hiện có trên máy

    blkid

### FAT32

    mlabel -i <device> ::<label>

### NTFS

    ntfslabel <device> <label>
