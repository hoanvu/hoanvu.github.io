---
layout: post
title: "CentOS does not recognize new network card"
date: 2013-07-17 11:58:20 +0700
categories: system_admin linux
tags: system_admin network centos
---

I didn't have chance to test this with physical machines, but after adding a new network card to a virtual CentOS node in VMWare Workstation 8, the server will not recognize the newly added device. In this post I will show you how to fix this problem.

Firstly, in my VMWare Workstation, I installed a fresh CentOS machine with a single network card, called `eth0`. Below is the result of the `ifconfig` command:

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

Now, let's the second network card to the server, called `eth1` from VMWare. When you type `ifconfig` in the terminal, the result is still the same:

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

In fact, the second network card was successfully added to the server, but you have to use the option `-a` in order to see it:

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

To be able to use this new network card, you need to create a configuration file for it, name the file as `ifcfg-eth1` in the directory `/etc/sysconfig/network-scripts/` with the following contents:

```
DEVICE=eth1
HWADDR=00:0C:29:B3:55:44
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=yes
BOOTPROTO=dhcp
```

Note that the value for `HWADDR` must be taken from the command `ifconfig -a` above. Save and close the file, and restart the network service:

```
service network restart
```

Now type `ifconfig`, without option `-a`, the `eth1` card will show up:

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

Note that if you mistype or give the incorrect value for the `HWADDR` line in the configuration file of `eth1` (`/etc/sysconfig/network-scripts/ifcfg-eth1`), you will see the following error while restarting the network service:

```
Bringing up interface eth1: Device eth1 has different MAC address than expected, ignoring.
[FAILED]
```