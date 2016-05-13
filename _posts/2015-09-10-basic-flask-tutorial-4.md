---
layout: post
title: "Basic Flask Tutorial - 4"
date: 2015-09-10 21:00:23 +0700
categories: python flask
tags: python web flask tutorial
---

## Phần 4: Template và Database

#### Mục lục 
1. [Giới thiệu](https://hoanvu.github.io/2015/09/basic-flask-tutorial-1)
2. [Cài đặt và chuẩn bị môi trường](https://hoanvu.github.io/2015/09/basic-flask-tutorial-2)
3. [Xây dựng bộ khung cho một ứng dụng Flask](https://hoanvu.github.io/2015/09/basic-flask-tutorial-3)
4. [Template và Database](https://hoanvu.github.io/2015/09/basic-flask-tutorial-4)
5. [Xây dựng các tính năng chính của hệ thống](https://hoanvu.github.io/2015/09/basic-flask-tutorial-5)
<br><br>

#### Tìm hiểu về Jinja template

Các bạn có thể truy cập <a href="http://jinja.pocoo.org/docs/dev/">vào đây để đọc tài liệu chi tiết của Jinja</a>. Phần này mình sẽ giới thiệu qua một chút về template engine này, đủ để các bạn có thể đọc và hiểu source code của project. 

[Phần trước](https://hoanvu.github.io/2015/09/basic-flask-tutorial-3), mình đã giới thiệu tới các bạn hàm `render_template()` để render giao diện từ file HTML:

```python
    return render_template('index.html')
```

Ngoài tên của template được đưa vào ở tham số thứ nhất (ở đây là **index.html**), hàm `render_template()` còn cho phép chúng ta đưa vào các tham số khác giúp template có thể hiển thị tùy biến dựa vào một điều kiện hoặc biến được đưa vào. 

Ví dụ trong **server.py** mình có một list các server với tên như sau:

```python
serverList = ['google.com', 'wordpress.com', 'quora.com', 'vnexpress.net', 'dantri.com.vn']
```

và mình muốn hiển thị danh sách này ra trang chủ dưới dạng một unordered-list, mỗi server một dòng thì làm thế nào? 

Nếu như bài toán đặt ra đơn giản là hãy in ra console danh sách này dùng lệnh `print`, bạn sẽ biết ngay là sẽ phải dùng `for` loop:

```python
for server in serverList:
    print server
```

Cũng tương tự như thế, Jinja2 cung cấp cho chúng ta một vòng lặp for để có thể chạy qua tất cả các giá trị trong một list và in ra. Cách dùng sẽ y hệt như dùng một vòng lặp `for` thông thường, tất nhiên là trông sẽ hơi loằng ngoằng một chút thôi. Vòng lặp `for` trong Jinja template sẽ có cú pháp như sau:

<pre><code>
{&percnt; if em_yêu_thích_chó %}
    &lt;p> Mua Chó </p>
{&percnt; elif em_yêu_thích_mèo %}
    &lt;p> Mua Mèo </p>
{&percnt; elif em_yêu_thích_SH %}
    &lt;h3> Mua SH </h3>
{&percnt; else %} &lt;!-- chắc là thích ô tô -->
    &lt;h1> Hết tiền </h1>
{&percnt; endif %}
</code></pre>

Có thể ban đầu bạn sẽ cảm thấy hơi khó hiểu cú pháp này, mình cũng thế. Nhưng chỉ sau vài lần viết là sẽ quen. Chỉ cần lưu ý là không giống Python, Jinja yêu cầu bạn phải chỉ định điểm kết thúc của for loop bằng <code>{&percnt; endfor %}</code> hoặc câu điều kiện if dùng <code>{&percnt; endif %}</code>

Vậy file template HTML làm cách nào để có thể lấy được biến <strong>serverList</strong> như trong for loop ở phía trên? Chúng ta cho phép template nhận biến này bằng cách đưa tham số đó vào trong hàm `render_template()`

Trong <strong>server.py</strong>:

```python
@app.route('/')
def index():
    serverList = ['google.com', 'wordpress.com', 'quora.com', 'vnexpress.net', 'dantri.com.vn']

    return render_template('index.html', serverList=serverList)
```

Bằng cách truyền tham số <strong>serverList</strong> vào hàm `render_template()` như trên, chúng ta có thể tùy ý sử dụng tham số này trong template.

Trong template chúng ta cũng có thể truy cập vào các object như `request`, `session` hay `g` của Flask. Mình sẽ nói qua về các object này trong những phần tới.

Template thực sự trở nên rất hữu ích và phát huy tối đa sức mạnh của nó khi được sử dụng trong Template Inheritance. Mình giới thiệu về lí thuyết này trong phần dưới.

Trong project mà chúng ta sẽ viết, trên thanh navigation bar, bạn sẽ muốn hiển thị đường link để <strong>Login</strong> khi user chưa đăng nhập và nếu user đã đăng nhập thì sẽ hiển thị <strong>Logout</strong>. Mình không biết đối với các ngôn ngữ khác thế nào, nhưng bạn có thể làm điều này rất dễ dàng với Jinja:

<pre><code>
{&percnt; if not session.logged_in %}  <!-- if user not logged in, show Login link -->
    &lt;p class="navbar-text navbar-right login"> &lt;a href="/login">
        Login (default: &lt;strong>admin&lt;/strong> / &lt;strong>admin&lt;/strong>)&lt;/a> 
    &lt;/p>
{&percnt; else %}  <!-- otherwise, show logout link -->
    &lt;p class="navbar-text navbar-left"> &lt;a href="/addUser"> Add User &lt;/a> &lt;/p>
    &lt;p class="navbar-text navbar-right logout"> &lt;a href="/logout"> Logout &lt;/a> &lt;/p>
{&percnt; endif %}
</code></pre>

`session`, cũng giống `render_template()` hay `url_for()`, sẽ phải được import nếu bạn muốn sử dụng:

```python
from flask import session, ...
```

`session` là một object của Flask, cho phép chúng ta lưu thông tin của người dùng khi họ truy cập vào ứng dụng. `session` mã hóa cookies, cho phép người dùng có thể nhìn nhưng không thể chỉnh sửa cookies, trừ khi người dùng biết được khóa bảo mật được dùng để mã hóa. 

<strong>Khóa bảo mật, giống như một tham số cấu hình à?</strong> Đúng vậy, bạn cần phải cấu hình tham số này (`SECRET_KEY`) để có thể sử dụng session. Vậy bạn đã biết để tham số này ở đâu chưa? Cũng đúng luôn, chúng ta sẽ để nó ở trong <strong>config.cfg</strong> và bạn nhớ là hãy viết in hoa nhé:

```
SECRET_KEY = 'Cực_kỳ_bảo_mật'
```

Một <strong>SECRET_KEY</strong> càng an toàn thì càng phải mang tính ngẫu nhiên. Bạn có thể sử dụng hàm <strong>os.urandom()</strong> của Python để làm việc này. Hàm <strong>os.urandom()</strong> sử dụng bộ sinh số ngẫu nhiên của chính hệ điều hành để tạo ra một chuỗi số ngẫu nhiên cho bạn:

```
>>> import os
>>> os.urandom(24)
'H<"\x7f\xfd\x9dz\xaa\xba\x92\n}p\x9eC\xb8fl\xdc_\xd9\x92v0'
```
Sau đó hãy copy & paste chuỗi này vào trong file <strong>config.cfg</strong> là được:

```
SECRET_KEY = 'H<"\x7f\xfd\x9dz\xaa\xba\x92\n}p\x9eC\xb8fl\xdc_\xd9\x92v0'
```
<br>

#### Template Inheritance
Đây được coi là tính năng mạnh nhất của Jinja. Template Inheritance cho phép bạn xây dựng một template chung, bao gồm tất cả những phần phổ biến nhất của ứng dụng và định nghĩa ra các <strong>block</strong> mà các template con có thể ghi đè lên.

Ví dụ, trong project này hay bất kì website nào khác, phần header và footer thường là những phần phổ biến nhất. Header và footer thường xuất hiện trong tất cả các URL. Chính vì thế rất hợp lí nếu cho 2 phần này vào một template "mẹ", và các phần khác ở trong các template con. 

Đầu tiên các bạn hãy xóa toàn bộ nội dung trong template <strong>index.html</strong> mà chúng ta đã viết ở phần trước, và copy chúng vào trong một file template mẹ, gọi là <strong>layout.html</strong>. Cây thư mục của chúng ta sẽ như sau:

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
        layout.html
```

Đây là nội dung của file template mẹ <strong>layout.html</strong>:

<pre><code>
&lt;!doctype html>
&lt;title>Server Monitoring</title>

&lt;link rel="stylesheet" href="&lcub;&lcub; url_for('static', filename='bootstrap.min.css') }}">
&lt;link rel="stylesheet" href="&lcub;&lcub; url_for('static', filename='style.css') }}">

&lt;div class="container">
    &lt;nav class="navbar navbar-default">
        &lt;div class="container-fluid">
            &lt;a class="navbar-brand" href="/">Server Monitoring</a>
            {&percnt; if not session.logged_in %}  &lt;!-- if user not logged in, show Login link -->
                &lt;p class="navbar-text navbar-right login"> &lt;a href="/login">
                    Login (default: &lt;strong>admin</strong> / &lt;strong>admin</strong>)&lt;/a> 
                &lt;/p>
            {&percnt; else %}  &lt;!-- otherwise, show logout link -->
                &lt;p class="navbar-text navbar-left"> &lt;a href="/addUser"> Add User &lt;/a> &lt;/p>
                &lt;p class="navbar-text navbar-right logout"> &lt;a href="/logout"> Logout &lt;/a> &lt;/p>
            {&percnt; endif %}
        &lt;/div>
    &lt;/nav>

    &lt;!-- Sub template -->
    {&percnt; block body %} {&percnt; endblock %}
    
    &lt;hr>
    &lt;footer>
        &lt;p class="text-muted text-center credit">Simple Server Monitoring System</p>
    &lt;/footer>
&lt;/div>

&lt;script src="&lcub;&lcub; url_for('static', filename='jquery.min.js') }}"></script>
&lt;script src="&lcub;&lcub; url_for('static', filename='main.js') }}"></script>
</code></pre>

Bạn sẽ để ý thấy hầu hết nội dung trong <strong>layout.html</strong> sẽ không khác mấy so với <strong>index.html</strong>, ngoài việc load thêm các file `.js` và `.css`, điểm rõ nhất đó là việc thêm vào dòng này:

<pre><code>
{&percnt; block body %} {&percnt; endblock %}
</code></pre>

Bằng việc "thừa kế" template <strong>layout.html</strong> bằng các template con, block này cho phép ghi đè nội dung từ các template con tại đây, tất cả các phần khác sẽ được giữ nguyên.

Vậy thừa kế thế nào? Hiện tại chúng ta đã xóa toàn bộ nội dung của <strong>index.html</strong>, bước tiếp theo chúng ta sẽ biến <strong>index.html</strong> thành một template con của <strong>layout.html</strong>, thừa hưởng toàn bộ phần header và footer của <strong>layout.html</strong> và chèn phần thông tin server và trạng thái vào giữa.

<pre><code>
{&percnt; extends "layout.html" %}
{&percnt; block body %}

{&percnt; endblock %}
</code></pre>

Chuỗi loằng ngoằng ở dòng đầu tiên <strong><code>{&percnt; extends "layout.html" %}</code></strong> chỉ định rằng template này là một template con của <strong>layout.html</strong>, toàn bộ nội dung sau đó bên trong <strong><code>{&percnt; block body %} {&percnt; endblock %}</code></strong> sẽ được ghi đè lên <strong>layout.html</strong>. Lưu ý là <strong>body</strong> chính là tên của block sẽ bao gồm nội dung sẽ được ghi đè từ template con, tên này phải giống nhau từ cả template mẹ và con.

Dưới đây là toàn bộ nội dung của <strong>index.html</strong>

<pre><code>
{&percnt; extends "layout.html" %}
{&percnt; block body %}

    {&percnt; if session.logged_in %}
        &lt;form action="{{ url_for('add_server') }}" method=post>
            &lt;dl>
                &lt;strong>Server Name: </strong>
                &lt;input type="text" size=20 name=name class="input">
                &lt;input type="submit" value="Add" class="btn btn-primary btn-sm">
            &lt;/dl>
        &lt;/form>
    {&percnt; endif %}

    &lt;div id="content">
        &lt;table class="table table-striped">
                &lt;tr>
                    &lt;th class="header">SERVER</th>
                    &lt;th class="header">STATUS</th>  
                    &lt;th class="header">ACTION</th>          
                &lt;/tr>

            {&percnt; for server in serverList %}      
                &lt;tr> 
                    &lt;td class="server-name"> {{ server.serverName }} </td> 
                    {&percnt; if server.status == 0 %}
                        &lt;td class="online"> Online </td>
                    {&percnt; else %}
                        &lt;td class="offline"> Offline </td>
                    {&percnt; endif %}

                    &lt;td>
                        &lt;form action="/removeServer/{{server.id}}" method="post">
                            &lt;!-- Only allow logged in user to remove server -->
                            {&percnt; if session.logged_in %}
                                &lt;input type="submit" value="Remove" class="btn btn-danger btn-sm">
                            {&percnt; else %}
                                &lt;input type="submit" value="Remove" class="btn btn-danger btn-sm" disabled>
                            {&percnt; endif %}
                        &lt;/form>
                    &lt;/td>
                &lt;/tr>   
            {&percnt; endfor %}
        &lt;/table>
    &lt;/div>
{&percnt; endblock %}
</code></pre>

<strong>index.html</strong> sẽ kiểm tra nếu user đã đăng nhập hay chưa. Nếu đúng thì sẽ hiển thị một form cho phép user thêm user để theo dõi, nếu không sẽ ẩn form này đi. Sau đó sẽ hiển thị danh sách toàn bộ server đang có trong database, nút <strong>Remove</strong> để xóa server sẽ bị ẩn đi nếu user chưa đăng nhập.
<br><br>

#### Kết nối tới database
<a href="http://hoanvu.github.io/2015/09/basic-flask-tutorial-3">Như trong phần trước</a>, chúng ta đã tiến hành phân tích xem database cần có những gì và kết quả là đã có một file <strong>schema.sql</strong> được tạo ra ngay trong thư mục <strong>server_monitoring</strong>. Phần này chúng ta sẽ tiếp tục tìm hiểu xem làm thế nào để import file này vào database, và kết nối tới database như thế nào.

Đầu tiên hãy tạo một thư mục tên là <strong>db</strong> trong <strong>server_monitoring</strong> để chứa database của hệ thống. Cây thư mục của chúng ta lúc này sẽ như sau:

```
server_monitoring\
    server.py
    config.cfg
    schema.sql
    db\
    static\
        bootstrap.min.css
        jquery.min.js
    templates\
        index.html
        layout.html
```

Mỗi lần user truy cập vào hệ thống của chúng ta, Flask sẽ phải tự động mở một kết nối tới database và hiển thị danh sách server cùng trạng thái của chúng. Để xử lí vấn đề này, chúng ta sẽ viết một hàm kết nối tới database, và sử dụng hàm này trong một object rất đặc biệt cho phép tự động mở một kết nối tới database và truy vấn: object `g`. Trong <strong>server.py</strong>:

```python
def connect_db():
    return sqlite3.connect(app.config['DATABASE'])
```

Mỗi khi hàm `connect_db()` được gọi, chúng ta sẽ dùng hàm `connect()` được cung cấp bởi thư viện `sqlite3` với một tham số được truyền vào là đường dẫn tới file database được cấu hình trong tham số `DATABASE`. Có 2 điều cần lưu ý ở đây:

+ Bạn sẽ phải import thư viện <strong>sqlite3</strong> vào <strong>server.py</strong>

    ```
    import sqlite3
    ```

+ Dễ dàng nhận thấy DATABASE ở đây là một tham số cấu hình, tham số này có giá trị là đường dẫn tới file `.db`. Bạn hãy update vào file <strong>config.cfg</strong> như sau:

    ```
    DATABASE = "db/servers.db"
    ```

Tiếp theo, có vài cách để import file <strong>schema.sql</strong> vào SQLite3 database. Cách thông thường nhất là cài đặt SQLite3 và dùng lệnh import từ shell của nó. 

```
sqlite3 db/servers.db < schema.sql
```

Tuy nhiên cách này như chúng ta thấy, cần SQLite3 được cài đặt trước trên hệ thống, cùng với việc gõ lệnh với đường dẫn thư mục sẽ dễ dàng khiến chúng ta mắc lỗi. Cách tốt hơn là chúng ta sẽ viết hàm để kết nối tới database và import file <strong>schema.sql</strong> vào database khi hàm đó được gọi.

Việc này cần hỗ trợ bởi hàm <strong>closing()</strong> của thư viện <strong>contextlib</strong>, hãy import nó vào trong <strong>server.py</strong>:

```python
from contextlib import closing
```

Tiếp theo chúng ta sẽ viết một hàm tên là `init_db()`, có nhiệm vụ import toàn bộ nội dung của <strong>schema.sql</strong> vào SQLite database:

```python
def init_db()
    with closing(connect_db()) as db:
        with app.open_resource('schema.sql', mode='r') as f:
            db.cursor().executescript(f.read())

        db.commit()
```

Hàm `closing()` kết hợp với `with` cho phép chúng ta giữ kết nối liên tục tới database. Hàm `open_resource()` cung cấp bởi Flask đọc nội dung của <strong>schema.sql</strong>. `closing()` trả về một cursor cho phép chúng ta thực hiện việc thực thi nội dung của file <strong>schema.sql</strong> từng dòng một và ghi vào database.

Trước khi bật server, bạn hãy gọi hàm đó để init database trong Python shell:

```python
>>> from server import init_db
>>> init_db()
```

Hàm này khi được gọi sẽ tạo ra file <strong>servers.db</strong> trong thư mục <strong>db</strong> như đã được cấu hình trong `DATABASE`.

Vấn đề tiếp theo của chúng ta, là làm cách nào để xử lí việc kết nối tới database một cách hiệu quả. Là thế nào? Tức là với mỗi truy vấn của user vào hệ thống, một kết nối tới database sẽ được tạo, và kết nối này sẽ phải được tự động ngắt đi khi user thoát khỏi hệ thống. Flask cho phép chúng ta xử lí vấn đề này bằng 3 decorator: `before_request`, `after_request` và `teardown_request`

Trong <strong>server.py</strong>, ngay sau hàm `init_db()` và `connect_db()`, bạn hãy thêm code sau:

```python
...
def connect_db():
...
def init_db():
...
@app.before_request
def before_request():
    g.db = connect_db()

@app.teardown_request
def teardown_request(exception):
    db = getattr(g, 'db', None)
    if db is not None:
        db.close()
```

Hàm `before_request()` sẽ được gọi trước khi user truy vấn vào hệ thống. Hàm `after_request()` được gọi sau khi truy vấn, với 1 tham số truyền vào là response sẽ trả về cho user. Nhưng do hoạt động của hàm này không ổn định, nên thay vào đó hàm `teardown_request()` sẽ được dùng. 

Như đề cập ở phía trên, mỗi kết nối tới database cho một truy vấn của người dùng sẽ được lưu vào một object đặc biệt của Flask tên là `g`. Object này lưu trữ thông tin cho 1 truy vấn, như kết nối tới database chả hạn. `g` cho phép chúng ta thực hiện các thao tác truy vấn tới db và trả về kết quả tương ứng với mỗi user khi họ những tác vụ khác nhau trên hệ thống: user A muốn xem thông tin server, user B muốn xem toàn bộ user đang có, ...

Để sử dụng `g`, bạn cũng phải import từ Flask:

```
from flask import g, ...
```

### Tóm tắt
Trong phần này, chúng ta đã tìm hiểu thêm về Jinja Template Engine đi kèm với Flask. Cách sử dụng các câu điều kiện, loop trong template như thế nào. Chúng ta đã học cách thiết kế template một cách hiệu quả sử dụng tính năng rất mạnh mẽ của Jinja là Template Inheritance, trong đó các phần giao diện chung nhất của ứng dụng sẽ được cho vào một template mẹ, và các template con sẽ ghi đè lên một cách tùy ý trong các phần khác của giao diện.

Chúng ta cũng tìm hiểu khá nhiều về cách init database, kết nối tới database ra sao và việc xử lí những kết nối này một cách hiệu quả.

Phần sau sẽ chủ yếu là code vì lúc này bạn đã có đủ kiến thức cơ bản về Flask rồi, chúng ta sẽ viết những tính năng chính của hệ thống như đã đề cập ở <a href="http://hoanvu.github.io/2015/09/basic-flask-tutorial-1" target="_blank">Phần 1</a>.

<strong><a href="http://hoanvu.github.io/2015/09/basic-flask-tutorial-5">Phần cuối: Xây dựng các tính năng chính của hệ thống</a></strong>