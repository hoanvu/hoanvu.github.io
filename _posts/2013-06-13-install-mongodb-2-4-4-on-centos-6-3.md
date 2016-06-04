---
layout: post
title: "Install MongoDB 2.4.4 on CentOS 6.3"
date: 2013-06-13 11:58:20 +0700
categories: system_admin linux
tags: system_admin mongodb
---

In this post I will guide you to install MongoDB 2.4.4 on CentOS 6.3:
<br><br>

#### 1. Download MongoDB source

```
http://www.mongodb.org/downloads
```
<br>

#### 2. Save the downloaded file at /opt/setup
It's not compulsory that you have to save it at `/opt/setup`, but then you need to `cd` to the exact folder in step 3
<br><br>

#### 3. Extract the installation files

```
cd /opt/setup
tar -xvzf mongodb-linux-x86_64-2.4.4.tgz
```
<br>

#### 4. Move the extracted folder to /opt/ (it's HOME folder for MongoDB)

```
cd /opt/setup
mv mongodb-linux-x86_64-2.4.4 /opt/mongodb
```
<br>

#### 5. Create necessary directories like data, log for MongoDB

```
cd /opt/mongodb
mkdir data logs
```
<br>

#### 6. Create a config file and add configuration to it

```
touch /opt/mongodb/mongodb.conf
```

Add the following contents:

```
logpath = /opt/mongodb/logs/mongodb.log
logappend = true
dbpath = /opt/mongodb/data
fork = true
verbose = true
rest = true
```

Where: 

```
logpath: file chứa MongoDB log
logappend: append log vào file thay vì tạo file mới
dbpath: folder chứa database
fork: option chỉ định sẽ chạy MongoDB như 1 daemon
verbose: lắm mồm
rest: enable giao diện chứa thông tin cơ bản & lệnh của MongoDB, interface REST có thể đc xem bằng cổng 28017
```
<br>

#### 7. Create user and group for running MongoDB (run with non-root user)

```
groupadd mongodb
useradd -g mongodb mongodb
```
<br>

#### 8. Change the permission for MongoDB folder

```
chown -R mongodb:mongodb /opt/mongodb
```
<br>

#### 9. Let's run

```bash
su - mongodb
/opt/mongodb/bin/mongod --fork --config /opt/mongodb/mongodb.conf
```

Where:

```
--fork: chạy MongoDB như 1 daemon process
--config: lấy thông tin cấu hình trong file config
```