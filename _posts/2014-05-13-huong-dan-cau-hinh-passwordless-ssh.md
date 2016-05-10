---
layout: post
title: "Hướng dẫn cấu hình passwordless SSH"
date: 2014-05-13 10:20:20 +0700
categories: system_admin
tags: system_admin passwordless_ssh
---

Trong một số trường hợp bạn cần truy cập từ một Linux server sang một Linux server khác mà không muốn phải điền password. Ví dụ:

+ Đồng bộ dữ liệu từ 1 server sang nhiều server sử dụng rsync
+ Quản lí hệ thống bao gồm một lượng lớn thiết bị
+ Thực hiện tác vụ nào đó cần truy cập từ xa sử dụng shell script
+ ...

Để dễ tưởng tượng, mình sẽ thực hiện cấu hình như mô hình dưới. Bạn đứng từ server A và muốn truy cập SSH vào server B mà không phải điền password. Việc cấu hình sẽ được thực hiện trên server A.
<br><br>

<p align="center"><img src="http://127.0.0.1:4000/images/passwordless-ssh.jpg"></p>

Môi trường: **CentOS 6.4**
<br><br>

#### 1. Tạo public & private key

```
[root@ServerA ~]# ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
64:67:70:66:98:c4:d5:34:e9:ec:a2:f6:50:ce:8c:e8 root@ServerA
The key’s randomart image is:
+–[ RSA 2048]—-+
| oo+=oo. |
| += o. |
| o oo |
| o o o |
| S .. |
| . *. . |
| . o.+. |
| . o. |
| E. .. |
+—————–+
```

Ở mục điền passphrase, không cần gõ gì cả, chỉ cần ấn Enter là được.

Lệnh ssh-keygen sẽ tạo ra 1 cặp gồm 1 public key và 1 private key cho server A. Bước tiếp theo chúng ta chỉ việc copy public key của `ServerA` vào file `.ssh/authorized_keys` của `ServerB`. Hay nói cách khác là bảo `ServerB` rằng `ServerA` luôn được phép truy cập với public key đã trao đổi mà không cần hỏi password.
<br><br>

#### 2. Copy public key

```
[root@ServerA ~]# ssh-copy-id -i .ssh/id_rsa.pub root@ServerB
root@ServerB’s password:
Now try logging into the machine, with “ssh ‘root@ServerB'”, and check in:

.ssh/authorized_keys to make sure we haven’t added extra keys that you weren’t expecting.
```

Gõ lại password của ServerB khi được hỏi, nếu chính xác thì lệnh `ssh-copy-id` sẽ làm các việc còn lại và thông báo bạn thử truy cập vào `ServerB`.

Thông thường nếu bạn không muốn dùng lệnh `ssh-copy-id` thì có thể dùng scp để copy bằng tay nội dung của file `id_rsa.pub` vào file `authorized_keys`.

Lưu ý: với các bước cấu hình như trên, các bạn chỉ có thể dùng user `root` trên `ServerA` để truy cập vào `ServerB` bằng user `root`. Nếu bạn thay đổi user trên 1 trong 2 server thì vẫn sẽ bị hỏi password. Vì thế nếu muốn dùng user khác các bạn vẫn sẽ phải cấu hình cho user đó.