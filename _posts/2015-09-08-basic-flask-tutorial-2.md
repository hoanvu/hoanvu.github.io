---
layout: post
title: "Basic Flask Tutorial - 2"
date: 2015-09-08 8:13:24 +0700
categories: python flask
tags: python web flask tutorial
---

## Phần 2: Cài đặt và chuẩn bị môi trường

#### Mục lục 
1. [Giới thiệu](https://hoanvu.github.io/2015/09/basic-flask-tutorial-1)
2. [Cài đặt và chuẩn bị môi trường](https://hoanvu.github.io/2015/09/basic-flask-tutorial-2)
3. [Xây dựng bộ khung cho một ứng dụng Flask](https://hoanvu.github.io/2015/09/basic-flask-tutorial-3)
4. [Template và Database](https://hoanvu.github.io/2015/09/basic-flask-tutorial-4)
5. [Xây dựng các tính năng chính của hệ thống](https://hoanvu.github.io/2015/09/basic-flask-tutorial-5)
<br><br>

#### Version
Tutorial này sẽ sử dụng các framework với version sau:

+ <strong>Python</strong>: <em>2.7.10</em>
+ <strong>Flask</strong>: <em>0.10.1</em>
+ <strong>SQLite</strong>: <em>3.8.11.1</em>
+ <strong>Bootstrap</strong>: <em>3.3.5</em>
+ <strong>jQuery</strong>: <em>2.1.4</em>
+ <strong>Jinja</strong>: <em>2.8</em>

Nếu bạn chưa biết gì về những Bootstrap và jQuery thì cũng đừng lo lắng vì chúng được sử dụng rất ít, version nào được sử dụng mình nghĩ cũng không quan trọng lắm. Bạn có thể sử dụng version mới nhất của Bootstrap và jQuery nếu thích.
<br><br>

#### Cài đặt Flask

+ Mình coi như là bạn đã cài đặt Python trên máy tính rồi nên sẽ không cover việc cài đặt Python nữa. Chỉ lưu ý một chút là Flask recommend chúng ta sử dụng Python version 2.6 trở lên và hoạt động tốt nhất với Python 2.x. <a href="http://flask.pocoo.org/docs/0.10/python3/#python3-support" target="_blank">Nếu bạn muốn sử dụng Flask với Python 3.x thì click vào đây.</a>
+ Với SQLite thì thậm chí bạn không cần cài đặt. Tuy nhiên nếu bạn muốn thao tác trực tiếp với database trong quá trình viết code thì có thể <a href="https://www.sqlite.org/download.html" target="_blank">download tại đây</a>
+ Với Bootstrap và jQuery, thường thì những thư viện này được nhúng trực tiếp từ một CDN nào đó từ các nhà cung cấp. Tuy nhiên đối với project này thì mình recommend là nên download Bootstrap và jQuery về máy và nhúng trực tiếp vào code. Mục đích của Bootstrap là để thiết kế giao diện cho hệ thống, khi server mất kết nối tới CDN thì vẫn giữ được layout. jQuery được dùng để reload bảng chứa thông tin và trạng thái của server. Khi hệ thống mất kết nối tới CDN thì vẫn có thể reload được.
    + <a href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css" target="_blank">Download Bootstrap tại đây</a>
    + <a href="http://code.jquery.com/jquery-2.1.4.min.js" target="blank">Download jQuery tại đây</a>
+ Jinja sẽ đi kèm khi bạn cài đặt Flask

Các bài hướng dẫn trên internet thường recommend chúng ta nên cài đặt Flask sử dụng `virtualenv`. Nói nôm na thì `virtualenv` cho phép tạo ra một môi trường Python riêng biệt, không liên quan tới môi trường trên máy tính hoặc server của bạn. Việc này rất có lợi vì bạn có thể tha hồ nghịch ngợm ứng dụng của mình với các version và cấu hình khác nhau mà không làm ảnh hưởng tới môi trường thật. Tuy nhiên, do mình chưa thạo `virtualenv` nên sẽ không dám múa rìu qua mắt thợ và không cover trong bài viết này mà vẫn cài đặt Flask trên môi trường thật. 

Bạn có thể cài đặt Flask trong một nốt nhạc bằng pip:

```
pip install flask
```

+ `pip` cần quyền admin trên Windows hoặc root trên Unix/Linux để chạy. Trên Windows bạn có thể click chuột phải vào command prompt và chọn **Run as Administrator**. Trên Linux nếu bạn không có quyền root thì phải thêm `sudo` ở đầu (`sudo pip install flask`), tất nhiên là bạn vẫn phải có quyền `sudo`.
+ Nếu bạn chưa có `pip` trên máy, hãy <a href="https://pip.pypa.io/en/latest/installing.html" target="_blank">theo hướng dẫn này để cài đặt</a>.
<br><br>

#### Tạo thư mục cho project

Đầu tiên bạn hãy tạo một cây thư mục như sau:

```
server_monitoring\
    static\
    templates\
```

+ <strong>static</strong>: đây là folder chứa toàn bộ những static file của project như .js, .css, ... 
+ <strong>templates</strong>: khi render các template, Flask sẽ tự động tìm kiếm template trong thư mục <em>templates</em>. Nếu bạn không có folder này thì Flask sẽ báo lỗi. Đây là folder chứa toàn bộ file HTML của bạn

Như đã đề cập ở phía trên, mình recommend là nên download jQuery và Bootstrap về máy để sử dụng locally. Liệu bạn có đoán được là sẽ nên để chúng ở đâu chưa? Đúng rồi, bạn hãy copy chúng vào thư mục <em>static</em> để có thể nhúng vào code sau này. Ngoài ra, khi mới download về, jQuery sẽ có tên dạng như: <em>jquery-2.1.4.min.js</em>, bạn có thể bỏ dãy số version thành <em>jquery.min.js</em> cho tiện thao tác.

Như vậy, cây thư mục của chúng ta cho tới hiện tại sẽ như sau:

```
server_monitoring\
    static\
        bootstrap.min.css
        jquery.min.js
    templates\
```
Phần tiếp theo, chúng ta sẽ bắt đầu viết những dòng code đầu tiên. Cheers!
<br><br>

[**Phần 3: Xây dựng bộ khung cho một ứng dụng Flask &raquo;**](https://hoanvu.github.io/2015/09/basic-flask-tutorial-3)