---
layout: post
title: "Using Fingerprint Reader on Ubuntu"
date: 2016-05-28 10:07:30 +0700
categories: linux
tags: fingerprint_reader linux ubuntu
---

Today I saw a colleague using Fingerprint reader to login to his Ubuntu 14.04. I was also impressed when he did some installation using `apt-get` or `pip install`, the system asked him to swipe his finger across the fingerprint reader in order to proceed with the installation instead of entering password as normal. Even though I already used this technology a while ago with Windows 7, and the fact is that the convenient of this authentication method used to make me forget my password, but I couldn't keep myself from being fascinated with the cool message. So I decided to figure it out to install it on my system, and it's quite easy.

You might follow these simple steps to get it working. I'm using Dell Vostro 3560, so there's probability that it may be different comparing to your case.
<br><br>

#### Check if Fingerprint Reader is recognized on your system

```
lsusb
```

My output is as follow, notice the 6th line, my hardware is `Validity Sensors, Inc. VFS5011 Fingerprint Reader`

```
hoanvu@Hoan:~$ lsusb
Bus 004 Device 003: ID 0a5c:21d7 Broadcom Corp. BCM43142 Bluetooth 4.0
Bus 004 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 005: ID 0c45:643f Microdia Dell Integrated HD Webcam
Bus 003 Device 004: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 003 Device 003: ID 138a:0011 Validity Sensors, Inc. VFS5011 Fingerprint Reader
Bus 003 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 002: ID 03f0:094a Hewlett-Packard Optical Mouse [672662-001]
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
<br>

#### Install fPrint

```
$ sudo add-apt-repository ppa:fingerprint/fprint
$ sudo apt-get update
$ sudo apt-get install libpam-fprintd
```

You might be required to type in your account password before the installation begins.

To check whether the installation succeed, a file name **common-auth** should be created already in your system. Check the content of this file, you should see the following line:

```
$ grep fprint /etc/pam.d/common-auth
auth	[success=2 default=ignore]	pam_fprintd.so max_tries=1 timeout=10 # debug
```
<br>

#### Register your fingerprint

Use the following command to register your fingerprint, it will ask you to swipe your finger several times:

```
$ fprint-enroll
```

Keep swiping your finger until finish:

```
Using device /net/reactivated/Fprint/Device/0
Enrolling right-index-finger finger.
Enroll result: enroll-stage-passed
Enroll result: enroll-stage-passed
Enroll result: enroll-stage-passed
Enroll result: enroll-stage-passed
Enroll result: enroll-completed
```

And you are done. Now everytime you do something that require entering password like login, package installation, you will be prompted to swipe your finger to continue, like following:

```
$ sudo apt-get install ruby ruby-dev make gcc nodejs
Swipe your finger across the fingerprint reader
...
```

Enjoy!