---
layout: post
title: "(VN) Basic Flask Tutorial - 5"
date: 2015-09-11 10:45:44 +0700
categories: python flask programming
tags: python web flask tutorial
---

## Phần 5: Xây dựng các tính năng

#### Mục lục 
1. [Giới thiệu](https://hoanvu.github.io/2015/09/basic-flask-tutorial-1)
2. [Cài đặt và chuẩn bị môi trường](https://hoanvu.github.io/2015/09/basic-flask-tutorial-2)
3. [Xây dựng bộ khung cho một ứng dụng Flask](https://hoanvu.github.io/2015/09/basic-flask-tutorial-3)
4. [Template và Database](https://hoanvu.github.io/2015/09/basic-flask-tutorial-4)
5. [Xây dựng các tính năng chính của hệ thống](https://hoanvu.github.io/2015/09/basic-flask-tutorial-5)
<br><br>

Trong <a href="https://hoanvu.github.io/2015/09/basic-flask-tutorial-1" target="_blank">phần trước</a>, mình đã giới thiệu với các bạn những tính năng chính của Hệ thống theo dõi server mà chúng ta sẽ dựa vào đó để tìm hiểu các lí thuyết của Flask và cuối cùng là xây dựng một hệ thống hoàn chỉnh. Dưới đây là những tính năng của hệ thống:

+ Khi chưa đăng nhập, hiển thị toàn bộ server đang theo dõi cùng trạng thái
+ Đăng nhập 
+ Đăng xuất
+ Sau khi đăng nhập:
    + Thêm server để theo dõi
    + Thêm user quản trị
    + Xóa server đang theo dõi
    + Xóa user quản trị
+ Tự động gửi email khi phát hiện server down

<pre>
<strong>Lưu ý</strong>: Do quá dài nên mình sẽ không giải thích hết code, mà sẽ chỉ đề cập đến 1 số điểm quan trọng trong code 
của mỗi tính năng. Nếu bạn chưa hiểu có thể đọc lại những phần trước nhé.
</pre>
<br>

#### Hiển thị thông tin server

Thực ra chúng ta đã hoàn thành xong tính năng này ở phần trước khi tìm hiểu về template và database. Hiện tại khi user truy cập vào trang index của ứng dụng sẽ nhìn thấy 2 server đã có sẵn và trạng thái của chúng. Lí do là bởi vì chúng ta đã thêm 2 server này vào file <strong>schema.sql</strong>.

Đây là code phía backend, trong <strong>server.py</strong>:

```python
@app.route('/')
def index():
    cur = g.db.execute("select * from servers order by name")
    serverList = [dict(id=row[0], serverName=row[1], status=isAlive(row[1])) for row in cur.fetchall()]

    return render_template("index.html", serverList=serverList)
```

Còn nội dung của template <strong>index.html</strong> các bạn có thể xem ở <a href="http://127.0.0.1:4000/2015/09/basic-flask-tutorial-4" target="_blank">phần trước</a> nhé.

Đầu tiên hàm `execute()` sẽ trả về con trỏ với câu truy vấn tới database tương ứng. Sau đó sử dụng hàm `fetchall()` trên con trỏ này để lấy toàn bộ record trong database và lưu vào biến `serverList`. Do kết quả mà `fetchall()` trả về là tuple, nên chúng ta dùng hàm `dict()` để convert từ tuple về dict để tiện thao tác hơn. Hàm `isAlive()` có nhiệm vụ kiểm tra xem server đang up hay down và lưu vào property `status` của dict.

Trong template <strong>index.html</strong>, các bạn cũng lưu ý là navigation bar sẽ hiển thị Login hay Logout tùy vào việc user đã đăng nhập hay chưa, mình đã giải thích ở phần trước.

Thuật toán kiểm tra trạng thái của server trả về kết quả là 0 (online) hoặc khác 0 (offline) nên chúng ta sẽ phải convert các giá trị vô nghĩa này sang một dạng mà người dùng có thể hiểu được. Việc này được thực hiện trong <strong>index.html</strong> với đoạn code sau:

<pre><code>
{&percnt; if server.status == 0 %}
    &lt;td class="online"> Online </td>
{&percnt; else %}
    &lt;td class="offline"> Offline </td>
{&percnt; endif %}
</code></pre>
<br>

#### Đăng nhập / Đăng xuất

Hàm `login()` sẽ thực hiện các tác vụ sau:

+ Kiểm tra tên đăng nhập được điền vào có tồn tại không
    + Nếu không, in ra "Tên đăng nhập không tồn tại"
    + Nếu có tồn tại, kiểm tra mật khẩu được điền vào có khớp với tên đăng nhập không
        + Nếu không khớp, in ra "Sai mật khẩu"
        + Nếu khớp, cho phép user đăng nhập

Thuật toán không có gì đặc biệt, việc thực hiện đăng nhập cho user cũng vô cùng đơn giản là set giá trị của key `logged_in` của object `session` thành `True`:

```python
session['logged_in'] = True
```

Điểm lưu ý thứ 2 là trong decorator `route()`, chúng ta sẽ phải truyền vào tham số `methods`. Nếu như URL mà user đăng nhập vào không cần POST (không gửi dữ liệu lên server, như truy cập vào trang chủ chả hạn), thì không cần truyền vào tham số này. Flask sẽ check header trong request của user, nếu chỉ đơn thuần là GET, sẽ trả về trang đăng nhập, nếu là POST thì sẽ kiểm tra và đăng nhập user vào hệ thống. Chính vì thế chúng ta phải có thêm một bước kiểm tra HTTP method là gì:

```python
if request.method == 'POST':
```

`request` cũng là một object của Flask, cho phép chúng ta truy cập vào dữ liệu trong request của user, bạn cũng cần phải import object này:

```python
from flask import request, ...
```

Nếu user không thể đăng nhập, hệ thống sẽ dùng hàm `render_template()` để hiện thị lại trang login với lỗi tương ứng. Nếu user đăng nhập thành công thì sẽ được redirect về trang chủ bằng cách sử dụng hàm `redirect()` của Flask. Đúng rồi, lại phải import nó vào:

```python
from flask import redirect, ...
```

Đăng nhập thì set giá trị của key `logged_in` thành `True`, vậy để đăng xuất user ra thì chúng ta chỉ cần set giá trị của key này về `None` là xong. Nhưng chúng ta sẽ không set trực tiếp mà dùng hàm `pop()`. Hàm này cho phép chúng ta xóa key `logged_in` nếu nó đang tồn tại `session` hoặc không làm gì cả khi không tồn tại.

```python
session.pop('logged_in', None)
```

Toàn bộ source code của hàm `login()` và `logout()` các bạn xem trong file <strong>server.py</strong> nhé.
<br><br>

#### Thêm server

Chúng ta sẽ định nghĩa một route decorator lắng nghe tại `/addServer` và chỉ chấp nhận HTTP POST. Trong template <strong>index.html</strong>, chúng ta dùng câu điều kiện `if` của Jinja để kiểm tra xem user đã đăng nhập hay chưa, và chỉ khi đó form hiển thị cho phép user điền thông tin và thêm server mới hiện ra:

<pre><code>
{&percnt; if session.logged_in %}
    &lt;form action="&lcub;&lcub; url_for('add_server') }}" method=post>
        &lt;dl>
            &lt;strong>Server Name: </strong>
            &lt;input type="text" size=20 name=name class="input">
            &lt;input type="submit" value="Add" class="btn btn-primary btn-sm">
        &lt;/dl>
    &lt;/form>
{&percnt; endif %}
</code></pre>

Khi user điền thông tin server vào ô <strong>name</strong> và ấn nút <strong>Add</strong>, dữ liệu trong form này sẽ được gửi vào URL được sinh ra bởi hàm `url_for()`, mà cụ thể là URL được định nghĩa trong decorator phía trên, chính là `/addServer`. Đây là code thực hiện việc thêm server vào database:

```python
@app.route('/addServer', methods=['POST'])
def add_server():
    if not session.get('logged_in'):
        abort(401)

    g.db.execute("insert into servers (name) values (?)",
                                [request.form['name']])

    g.db.commit()
    return redirect(url_for('index'))
```

Đầu tiên, hàm `add_server()` sẽ kiểm tra user đã đăng nhập chưa và trả về lỗi 401 (Unauthorized) nếu user chưa đăng nhập. Sau đó `execute` câu truy vấn để thêm server vào hệ thống thông qua dữ liệu được điền trong form.

Sau khi server được thêm thành công, user sẽ được `redirect` về trang index để danh sách server vừa được cập nhật.
<br><br>

#### Xóa server

Việc xóa server khỏi hệ thống cũng tương tự như việc thêm vào hệ thống. Tuy nhiên có một điểm cần lưu ý là cấu trúc của URL mà hệ thống sẽ lắng nghe khi user ra lệnh cho hệ thống xóa một server bất kì. Đây là lúc chúng ta sử dụng đến `server ID`. Nếu bạn nhớ lại, trong khi thiết kế database, bảng `servers` có thêm một trường `server ID`, và chúng ta chỉ việc thêm thông tin ID này vào URL như một biến. Để đọc thêm về biến trong URL, các bạn hãy đọc lại Phần 3 nhé.

Đây là code của tính năng xóa server:

```python
@app.route('/removeServer/<serverId>', methods=['POST'])
def remove_server(serverId):
    if not session.get('logged_in'):
        abort(401)

    g.db.execute("delete from servers where id = ?", [serverId])
    g.db.commit()

    return redirect(url_for('index'))
```
<br>

#### Thêm/Xóa user quản trị

Việc thêm hay xóa user quản trị trên hệ thống cũng giống với tác vụ thêm hay xóa server. Chúng ta cũng sẽ có một template riêng cho việc liệt kê danh sách tất cả user đang có. Chỉ có một chút khác biệt so với việc liệt kê server, đó là do chỉ khi user đăng nhập mới nhìn thấy đường link dẫn tới trang quản trị user, nên chúng ta không cần phải viết logic trong template để kiểm tra xem user đã đăng nhập hay chưa rồi mới hiển thị form điền thông tin user mới mà sẽ hiển thị luôn. Nói đơn giản thì việc giấu form điền thông tin user là vô nghĩa vì lúc này user đã đăng nhập rồi.

Đầu tiên chúng ta sẽ kiểm tra xem tên đăng nhập mà user điền vào ô username đã tồn tại chưa. Nếu rồi thì trả về tin nhắn **"Tên đăng nhập đã tồn tại"**, còn nếu không thì dùng hàm `execute()` trên object `g` để thực hiện câu lệnh SQL insert user vào hệ thống.

Sau khi thêm user thành công, hệ thống tự động redirect sang trang liệt kê toàn bộ user

Xóa user cũng giống như logic cho việc xóa server. Chúng ta sẽ phải truyền tên đăng nhập của user cần xóa như một biến vào URL giống như truyền `server ID`:

```python
@app.route('/removeUser/<username>', methods=['POST'])
```

Source code chi tiết của việc thêm/xóa user các bạn xem hàm `add_user()` và `remove_user()` trong <strong>server.py</strong> nhé.
<br><br>

#### Gửi email khi phát hiện server down

Riêng phần này mình đã từng viết source code và giải thích chi tiết thuật toán <a href="https://github.com/hoanvu/python_projects/tree/master/network/sendEmail">tại đây</a> nên mình không nói lại chi tiết nữa (vì tính năng này cũng không liên quan tới Flask). Tuy nhiên có một số điểm mình sẽ note lại đây để cho bạn tiện đọc code:

+ Để gửi nhận mail trong Python chúng ta sẽ dùng thư viện `smtplib` và dùng Gmail để gửi. 
+ Thay vì lưu email nhận và gửi trong file, chúng ta sẽ lưu thông này như một tham số trong file <strong>config.cfg</strong>
+ Để gửi mail thông báo khi có server down, chúng ta sẽ phải thay đổi một chút trong hàm `index()`. Bởi vì mình dùng jQuery để refresh bảng chứa thông tin server 5s một lần, và dữ liệu trong bảng này được lấy từ hàm `index()`, nên sau mỗi 5s khi có server down hệ thống sẽ phải gửi email thông báo ngay lúc đó. Trong hàm `index()` các bạn hãy thêm đoạn code sau:

```python
for server in serverList:
    if server['status'] == 1:
        sendEmail(server['serverName'])
```

Hàm `sendEmail()` nhận 1 tham số truyền vào là tên server và sẽ gửi mail thông báo nếu server này down.
<br><br>

#### Wrap-up

Vậy là chúng ta đã kết thúc 5 phần dài đằng đẵng giới thiệu về Flask và xây dựng một hệ thống theo dõi server hoàn chỉnh. Chắc chắn là còn rất nhiều thiếu sót trong bài viết này và mình hi vọng nhận được feedback từ phía mọi người để chỉnh sửa và bổ sung. Bản thân mình đã học thêm được rất nhiều sau khi viết tutorial này và hi vọng bạn cũng thế.