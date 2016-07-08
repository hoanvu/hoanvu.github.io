---
layout: post
title: "(VN) Basic Flask Tutorial - 3"
date: 2015-09-09 22:22:44 +0700
categories: python flask programming
tags: python web flask tutorial
---

## Phần 3: Xây dựng bộ khung cho một ứng dụng Flask

#### Mục lục 
1. [Giới thiệu](https://hoanvu.github.io/2015/09/basic-flask-tutorial-1)
2. [Cài đặt và chuẩn bị môi trường](https://hoanvu.github.io/2015/09/basic-flask-tutorial-2)
3. [Xây dựng bộ khung cho một ứng dụng Flask](https://hoanvu.github.io/2015/09/basic-flask-tutorial-3)
4. [Template và Database](https://hoanvu.github.io/2015/09/basic-flask-tutorial-4)
5. [Xây dựng các tính năng chính của hệ thống](https://hoanvu.github.io/2015/09/basic-flask-tutorial-5)
<br><br>

Như mình đã đề cập trong mục <a href="https://github.com/hoanvu/basic_flask_tutorial#giới-thiệu-về-flask" target="_blank">Giới thiệu Flask</a>, bạn có thể chia nhỏ ứng dụng của mình ra thành nhiều file source Python khác nhau. Điều này giúp ích rất nhiều khi ứng dụng bắt đầu phình ra, và việc maintain hay debug cũng sẽ bớt đau đầu hơn. Tuy nhiên, do project này khá nhỏ, cộng với mục đích là giới thiệu cơ bản về Flask nên mình sẽ "keep it simple", và chỉ cho riêng phần config của app ra một file riêng, còn lại sẽ để code vào một file duy nhất: `server.py`.
<br><br>

#### Viết một ứng dụng tối giản

Đầu tiên bạn hãy tạo file tên là `server.py` ngay trong thư mục `server_monitoring`:

```
server_monitoring\
    server.py
    static\
        bootstrap.min.css
        jquery.min.js
    templates\
```

Và viết đoạn code sau trong <em>server.py</em> (mình recommend là nên tự viết lại, chứ không nên copy & paste, đó cũng là 1 cách học):

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def index():
    return "This is the index page!"

if __name__ == "__main__":
    app.run()
```

Sau đó trong command prompt(*), gõ lệnh sau để start server, bạn sẽ thấy Flask báo là server đã chạy và lắng nghe trên cổng 5000:

```python
python hello.py
    * Running on http://127.0.0.1:5000/
```

**(*)**: Mình dùng Windows tên từ nay về sau khi mình đề cập là "gõ lệnh sau" thì tức là mình đang làm trong Command Prompt. Nếu bạn dùng Unix/Linux thì có thể gõ trực tiếp trong shell

Bây giờ, mở bất kì trình duyệt web nào mà bạn thích và gõ trong thanh địa chỉ **http://127.0.0.1:5000**. Nếu bạn thấy tin nhắn <strong>This is the index page!</strong> hiển thị thì tức là bạn đã thành công trong việc viết ứng dụng Flask đầu tiên rồi.

Vậy ý nghĩa của mỗi dòng code trong <em>server.py</em> là gì?

1. Đầu tiên chúng ta import lớp Flask. Instance của lớp này sẽ chính là một ứng dụng <a href="http://wsgi.readthedocs.org/en/latest/what.html" target="_blank">WSGI</a>.
2. Sau đó chúng ta tạo một instance tên là `app` của lớp Flask vừa được import. Tham số `__name__` được truyền vào chính là tên của module hoặc package của ứng dụng. Tham số này giúp Flask biết sẽ tìm template và các file static của ứng dụng ở đâu.
3. Tiếp theo, chúng ta dùng `route()` <a href="https://www.jeffknupp.com/blog/2013/11/29/improve-your-python-decorators-explained/" target="_blank">decorator</a> để cho Flask biết nên làm gì khi user truy cập vào một trang bất kì của ứng dụng. Như ví dụ phía trên thì có thể hiểu nôm na là chúng ta đang nói: "<em>Flask ơi, nếu như user họ truy cập vào trang /, thì hãy thực thi hàm `index()`, ở đây đơn giản là trả về một tin nhắn để thông báo cho họ biết ứng dụng của chúng ta đã hoạt động.</em>". <br><br>Vậy chúng ta muốn chỉ định Flask làm thế này thì sao? "<em>Khi user truy cập vào **/login**, hãy thực thi hàm `login()`, và hàm này trả về một tin nhắn sau: **This is the login page**.</em>" (Tớ ko viết đâu, bài tập cho các bạn đấy)
4. Cuối cùng chúng ta sử dụng hàm `run()` để chạy một local server cho ứng dụng

Ấn `Ctrl+C` để stop server.
<br><br>

#### Biến trong URL

Thông thường các bạn hay thấy URL có dạng như 

```
http://monitor.com/server?name=test1&status=0
```

Phần phía sau dấu `?` được gọi là các biến và giá trị của chúng. Các biến được tách ra bởi kí tự `&`.

Jinja cho phép chúng ta tạo ra các URL có chứa các biến như vậy, dưới đây là một ví dụ:

```python
@app.route('/<serverName>')
def index(serverName):
    return "Hello, " + serverName
```

Khi user truy cập vào <strong>/Thor</strong>, <strong>'Hello, Thor'</strong> sẽ được trả về. 

Khi user truy cập vào <strong>/IronMan</strong>, <strong>'Hello, IronMan'</strong> sẽ được trả về.

Các bạn cũng đã hiểu vì sao gọi là biến, bởi vì cùng 1 URL nhưng kết quả trả về sẽ khác nhau tùy thuộc vào giá trị của biến được truyền vào URL.
<br><br>

#### Sử dụng template riêng

Bây giờ bạn thắc mắc: "<em>Tôi không muốn đơn thuần chỉ trả về 1 string vô nghĩa, tôi muốn hiển thị giao diện cụ thể khi người dùng truy cập vào homepage hay trang login thì làm thế nào?</em>"

Như các bạn đã biết, Flask sử dụng Jinja2 làm template engine. Và Jinja2 mặc định sẽ tìm các file template trong thư mục <em>templates</em>. Chính vì thế, bạn sẽ phải để toàn bộ các file HTML vào trong thư mục này.

Vậy để trả lời câu hỏi trên, chúng ta sẽ render một template cho trang index bao gồm tên ứng dụng, thanh navigation (login/logout) và footer. Hiện tại phần body sẽ chưa có gì do chưa có kết nối tới cơ sở dữ liệu. Trang index sau khi chúng ta render ra sẽ có giao diện như hình dưới:

![server monitoring first page](https://raw.githubusercontent.com/hoanvu/hoanvu.github.io/master/images/posts/server_monitoring_page1.JPG)

Để render một template từ file HTML, bạn phải sử dụng hàm `render_template()` của Flask, và việc đầu tiên bạn phải làm là import hàm này vào trong **server.py**

```python
from flask import Flask, render_template
```

Tiếp theo, trong thư mục <em>templates</em>, bạn tạo một file tên là <em>index.html</em> và copy (nếu bạn không muốn viết code HTML thì có thể copy) đoạn code sau vào trong đó:

```html
<!doctype html>
<title>Server Monitoring</title>

<link rel="stylesheet" href="{{ url_for('static', filename='bootstrap.min.css') }}">

<div class="container">
    <nav class="navbar navbar-default">
        <div class="container-fluid">
            <a class="navbar-brand" href="/">Server Monitoring</a>
                <p class="navbar-text navbar-right login"> <a href="/login">
                    Login (default: <strong>admin</strong> / <strong>admin</strong>)</a> 
                </p>
        </div>
    </nav>
    <br> <br> <br> <br> <br>
    <hr>
    <footer>
        <p class="text-muted text-center credit">Simple Server Monitoring System</p>
    </footer>
</div>
```

+ Nhìn vào code bạn có thể thấy chúng ta đã load file **bootstrap.min.css** để thiết kế giao diện ban đầu. Nhưng cái chuỗi loằng ngoằng `{{ url_for('static', filename='bootstrap.min.css') }}` bên trong `href` nghĩa là gì? Trong Jinja2, tất cả những gì được đặt bên trong `{{ }}` được coi là một expression và sẽ trả về output ra frontend. Ví dụ `{{ 1 + 2 }}` sẽ in ra `3` chẳng hạn. 
+ Hàm `url_for()` sẽ tự động tạo ra một URL với tham số thứ nhất gọi là endpoint, các tham số từ thứ 2 trở đi sẽ được nối vào sau của endpoint ở tham số thứ nhất. Vậy kết quả của cái loằng ngoằng đó sẽ thành <strong>static/bootstrap.min.css</strong> và cho phép `href` load Bootstrap vào **index.html**

Để dùng hàm url_for, chúng ta cũng sẽ phải import nó từ Flask:

```python
from flask import Flask, render_template, url_for
```

Trong hàm <em>index()</em> viết phía trên, bạn thay dòng sau:

```python
    return "This is the index page!"
```

bằng dòng sau:

```python
    return render_template('index.html')
```

Lưu **server.py**, khởi động lại server và truy cập vào **http://127.0.0.1:5000** để xem giao diện mà chúng ta vừa render cho trang index.

Trong hàm `render_template()`, chúng ta truyền vào tham số thứ nhất là tên của file template mà chúng ta muốn hàm `index()` render ra khi user truy cập vào "/". Flask sẽ tự động tìm kiếm trong thư mục **templates** để xem có file đó không và render ra giao diện tương ứng.
<br><br>

#### Cấu hình các tham số

Một ứng dụng Flask có thể được cấu hình các tham số khác nhau như: kết nối tới database, debug mode, username, password ... Về cơ bản bạn có thể để chung các cấu hình này trong file **server.py**, nhưng mình sẽ tách ra thành một file riêng gọi là **config.cfg**. Đối với những ứng dụng nhỏ như project này, việc tách ra sẽ không đem lại hiệu quả lớn, nhưng nó sẽ rất có ích đối với những project lớn khi có rất nhiều tham số.

Bạn hãy tạo file **config.cfg** ngay trong thư mục **server_monitoring**. Cây thư mục của chúng ta hiện tại sẽ như sau:

```
server_monitoring\
    server.py
    config.cfg
    static\
        bootstrap.min.css
        jquery.min.js
    templates\
        index.html
```

Ở phần trên, khi thay đổi hàm `index()`, nếu muốn server nhận các thay đổi trong source code, chúng ta sẽ phải tắt server và khởi động lại. Trong quá trình phát triển, chúng ta sẽ thay đổi source code liên tục để xem những thay đổi dù là nhỏ nhất có ảnh hưởng thế nào tới ứng dụng. Nếu phải làm đi làm lại việc này thì sẽ rất nhàm chán và mất thời gian. Flask cho phép bạn cấu hình để server tự động khởi động lại để nhận các thay đổi khi chúng ta lưu file source code. Tính năng này gọi là enable hay disable debug mode. Việc này chúng ta có thể gọi là cấu hình một tham số. Có vài cách để enable hay disable debug mode, tùy vào sở thích của mỗi người, nhưng mình nghĩ cách tốt nhất là cho tham số này vào file **config.cfg** để tiện quản lí và thay đổi khi cần.

**Lưu ý**: Bạn không bao giờ nên enable debug mode trong môi trường production vì debugger của Flask sẽ cho phép thực thi lệnh tùy ý trên chính giao diện của ứng dụng khi nó trả về lỗi. Chỉ sử dụng debug mode trong môi trường development

Bạn hãy mở file **config.cfg** và gõ dòng sau:

```python
DEBUG = True
```

Sau đó hãy gõ dòng sau vào ngay sau phần khai báo <em>app</em> trong <em>server.py</em>:

```python
...
app = Flask(__name__)
app.from_pyfile('config.cfg')
...
```

Hàm `from_pyfile()` sẽ nhìn vào file tham số được đưa vào, ở đây là **config.cfg** để tìm tất cả các biến được viết bằng chữ in hoa để cấu hình môi trường cho Flask. Lưu ý là <strong>dù dùng `from_pyfile()` hay bất kì hàm nào khác để load các tham số cấu hình, chúng ta buộc phải dùng các biến được viết in hoa</strong>. Ở đây là biến `DEBUG`. Nếu không, Flask sẽ không nhận các cấu hình này. Để thử bạn có thể thay `DEBUG` bằng `debug` hoặc `Debug` gì đó.

Sau đó, restart lại server lần cuối cùng, và sau lần này bạn sẽ không bao giờ phải tự restart nữa, Flask sẽ tự động làm thế mỗi khi phát hiện có thay đổi trong source code.

Khi khởi động server lên, bạn sẽ thấy có báo rằng từ nay server sẽ tự động restart:

```
python server.py
    * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
    * Restarting with stat
```

Sau này, khi mình viết các tham số dạng như `USERNAME = ...` hay `PASSWORD = ...` mà quên không đề cập thì bạn cũng biết là hãy đặt những dòng này trong **config.cfg** nhé.

Nếu bạn muốn truy cập các tham số cấu hình trong **config.cfg** từ **server.py** thì dùng:

```python
user = app.config["USERNAME"]
pass = app.config["PASSWORD"]
```

Tất cả tham số cấu hình được lưu trong list tên là `config`, một property của `app`.
<br><br>

#### Tạo Schema cho database

Bước tiếp theo, chúng ta sẽ thiết kế cơ sở dữ liệu của hệ thống. Project này bao gồm 2 đối tượng chính:

+ Danh sách server và trạng thái
+ Danh sách user để quản trị (thêm/bớt server, thêm/bớt user quản trị)

Đối với server, chúng ta sẽ không lưu trạng thái của server trong database. Trạng thái của server được kiểm tra và cập nhật sau mỗi 5s, nên nếu server up/down liên tục có thể sẽ khiến database bị overload khi số lượng server cần theo dõi lớn. Thay vào đó chúng ta sẽ viết một hàm để kiểm tra và trả về trạng thái tương ứng. Như vậy bảng chứa server sẽ chỉ cần 2 trường chính:

+ `Server ID`: primary key và autoincrement
+ `Server name`

Bảng chứa user sẽ bao gồm 2 trường:

+ `Username`: primary key
+ `Password`

Bạn hãy tạo một file tên là **schema.sql** ngay trong thư mục **server_monitoring** và gõ nội dung sau. Mình nghĩ là không cần phải giải thích nhiều mà các bạn sẽ tự hiểu được ý nghĩa của file này nếu như các bạn đã có chút kiến thức cơ bản về SQL:

```sql
drop table if exists servers;
drop table if exists users;
create table servers (
    id integer primary key autoincrement,
    name text not null
);

create table users (
    username text primary key,
    password text
);

insert into servers (name) values ('google.com');
insert into servers (name) values ('1.2.3.4');

insert into users values ('admin', 'admin');
```

Mỗi bảng chúng ta sẽ thêm vào một vài record để làm giá trị mặc định ban đầu.

Cây thư mục của chúng ta đến thời điểm hiện tại đang như sau:

```
server_monitoring\
    server.py
    config.cfg
    schema.sql
    static\
        bootstrap.min.css
        jquery.min.js
    templates\
        index.html
```
<br>

#### Vậy chúng ta đã có những gì rồi?

+ Chúng ta đã biết một ứng dụng Flask sẽ phải import lớp gì và một instance của lớp này sẽ chính là ứng dụng WSGI sẽ được xây dựng
+ Chúng ta đã biết cách render một template theo ý muốn bằng cách sử dụng hàm `render_template()`, toàn bộ template sẽ phải được để trong thư mục **templates**. Flask sử dụng Jinja2 làm template engine mặc định
+ Chúng ta đã biết cấu hình các tham số của Flask sử dụng một file riêng biệt và load bất kì một tham số nào khi cần. Tất cả các biến tham số sẽ phải được viết in hoa.
+ Chúng ta đã định nghĩa database sẽ cần có những thông tin gì, và tạo một file schema để sẵn sàng load vào database
<br><br>

[**Phần 4: Template và Database**](https://hoanvu.github.io/2015/09/basic-flask-tutorial-4)