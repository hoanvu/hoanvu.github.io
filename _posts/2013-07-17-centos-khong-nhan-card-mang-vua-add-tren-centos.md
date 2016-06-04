---
layout: post
title: "(VN) CentOS không nhận card mạng vừa add trên VMWare"
date: 2013-07-17 11:58:20 +0700
categories: system_admin linux
tags: system_admin network centos
---

Với máy thật mình chưa có dịp test, nhưng với máy ảo CentOS chạy trên VMWare Workstation 8, khi bạn add thêm một card mạng mới, server sẽ không tự động nhận card mạng mới vừa được add vào. Bài này mình sẽ hướng dẫn các bạn cách xử lí vấn đề này.

Đầu tiên, mình có 1 server CentOS 6.4 với 1 card mạng duy nhất là eth0. Kết quả của lệnh ```ifconfig``` trả về như sau:

```
[root@server2 ~]# ifconfig

eth0 Link encap:Ethernet HWaddr 00:0C:29:B3:55:3A
inet addr:192.168.0.106 Bcast:192.168.0.255 Mask:255.255.255.0
inet6 addr: fe80::20c:29ff:feb3:553a/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:81 errors:0 dropped:0 overruns:0 frame:0
TX packets:88 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:9482 (9.2 KiB) TX bytes:11909 (11.6 KiB)

lo Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:0 (0.0 b) TX bytes:0 (0.0 b)
```

Bây giờ mình tiến hành add thêm một card mạng eth1 vào server này từ VMWare workstation, lệnh ```ifconfig``` vẫn trả về như sau:

```
[root@server2 ~]# ifconfig

eth0 Link encap:Ethernet HWaddr 00:0C:29:B3:55:3A
inet addr:192.168.0.106 Bcast:192.168.0.255 Mask:255.255.255.0
inet6 addr: fe80::20c:29ff:feb3:553a/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:81 errors:0 dropped:0 overruns:0 frame:0
TX packets:88 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:9482 (9.2 KiB) TX bytes:11909 (11.6 KiB)

lo Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:0 (0.0 b) TX bytes:0 (0.0 b)
```

Lúc này, thực ra card mạng thứ 2 đã đc add thêm vào, tuy nhiên bạn phải dùng option -a mới thấy được, và card mạng này chưa sử dụng được trước khi được cấu hình:

```
[root@server2 ~]# ifconfig -a

eth0 Link encap:Ethernet HWaddr 00:0C:29:B3:55:3A
inet addr:192.168.0.106 Bcast:192.168.0.255 Mask:255.255.255.0
inet6 addr: fe80::20c:29ff:feb3:553a/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:147 errors:0 dropped:0 overruns:0 frame:0
TX packets:134 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:16414 (16.0 KiB) TX bytes:18145 (17.7 KiB)

eth1 Link encap:Ethernet HWaddr 00:0C:29:B3:55:44
BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:0 (0.0 b) TX bytes:0 (0.0 b)

lo Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:0 (0.0 b) TX bytes:0 (0.0 b)
```

Để có thể sử dụng được card mạng mới này, bạn cần phải tạo 1 file cấu hình tên là ```ifcfg-eth1``` tại ```/etc/sysconfig/network-scripts/``` với nội dung cơ bản như sau:

```
DEVICE=eth1
HWADDR=00:0C:29:B3:55:44
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=yes
BOOTPROTO=dhcp
```

Lưu ý là giá trị ở dòng ```HWADDR``` phải được lấy từ output của lệnh ```ifconfig -a```. Save và close lại, sau đó dùng lệnh:

```
service network restart
```

Đánh lại ifconfig, bạn sẽ thấy card mạng mới đã hiện lên và đã có thể sử dụng bình thường.

```
[root@server2 ~]# ifconfig

eth0 Link encap:Ethernet HWaddr 00:0C:29:B3:55:3A
inet addr:192.168.0.106 Bcast:192.168.0.255 Mask:255.255.255.0
inet6 addr: fe80::20c:29ff:feb3:553a/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:517 errors:0 dropped:0 overruns:0 frame:0
TX packets:452 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:50956 (49.7 KiB) TX bytes:101981 (99.5 KiB)

eth1 Link encap:Ethernet HWaddr 00:0C:29:B3:55:44
inet addr:192.168.0.107 Bcast:192.168.0.255 Mask:255.255.255.0
inet6 addr: fe80::20c:29ff:feb3:5544/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:10 errors:0 dropped:0 overruns:0 frame:0
TX packets:10 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:1756 (1.7 KiB) TX bytes:1236 (1.2 KiB)

lo Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:0 (0.0 b) TX bytes:0 (0.0 b)
```

Lưu ý: nếu trong file config của eth1 (```/etc/sysconfig/network-scripts/ifcfg-eth1```), bạn không sử dụng địa chỉ MAC từ output của ```ifconfig -a```, sau khi restart network bạn có thể sẽ gặp lỗi sau:

```
Bringing up interface eth1: Device eth1 has different MAC address than expected, ignoring.
[FAILED]
```