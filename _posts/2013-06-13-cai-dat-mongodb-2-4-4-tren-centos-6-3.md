---
layout: post
title: "Cài đặt MongoDB 2.4.4 trên CentOS 6.3"
date: 2013-06-13 11:58:20 +0700
categories: system_admin
tags: system_admin mongodb
---

Bài post này mình sẽ hướng dẫn các bạn cài đặt MongoDB trên CentOS:
<br><br>

#### 1. Download MongoDB source

```
http://www.mongodb.org/downloads
```
<br>

#### 2. Lưu file source tại /opt/setup
Các bạn có thể lưu ở bất kì đâu tùy ý, nhưng cần ```cd``` đến đúng thư mục đó trong bước 3.
<br><br>

#### 3. Giải nén

```
cd /opt/setup
tar -xvzf mongodb-linux-x86_64-2.4.4.tgz
```
<br>

#### 4. Copy folder vừa giải nén vào /opt (là HOME của MongoDB)

```
cd /opt/setup
mv mongodb-linux-x86_64-2.4.4 /opt/mongodb
```
<br>

#### 5. Tạo các folder cần thiết như data, log để chạy MongoDB

```
cd /opt/mongodb
mkdir data logs
```
<br>

#### 6. Tạo file config và thêm nội dung vào file config

```
touch /opt/mongodb/mongodb.conf
```

Thêm các nội dung sau:

```
logpath = /opt/mongodb/logs/mongodb.log
logappend = true
dbpath = /opt/mongodb/data
fork = true
verbose = true
rest = true
```

Trong đó: 

```
logpath: file chứa MongoDB log
logappend: append log vào file thay vì tạo file mới
dbpath: folder chứa database
fork: option chỉ định sẽ chạy MongoDB như 1 daemon
verbose: lắm mồm
rest: enable giao diện chứa thông tin cơ bản & lệnh của MongoDB, interface REST có thể đc xem bằng cổng 28017
```
<br>

#### 7. Tạo user & group mongodb (chạy với user thường)

```
groupadd mongodb
useradd -g mongodb mongodb
```
<br>

#### 8. Change quyền thư mục chứa MongoDB:

```
chown -R mongodb:mongodb /opt/mongodb
```
<br>

#### 9. Chạy thôi

```bash
su - mongodb
/opt/mongodb/bin/mongod --fork --config /opt/mongodb/mongodb.conf
```

Trong đó:

```
--fork: chạy MongoDB như 1 daemon process
--config: lấy thông tin cấu hình trong file config
```