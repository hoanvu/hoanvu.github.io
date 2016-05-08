---
layout: post
title: "Implicit và Explicit rating"
date: 2016-05-08 11:19:20 +0700
categories: data_mining
tags: data_mining implicit_rating explicit_rating
---

#### Lí thuyết

Implicit và Explicit rating là 2 thuật ngữ được dùng trong data mining. Trong quá trình sử dụng internet như: lướt web, mua sắm online, xem phim, nghe nhạc, ... người dùng sẽ thực hiện rất nhiều tác vụ khác nhau. Các tác vụ này có rất nhiều dạng khác nhau. Ví dụ:

+ click vào một đường link bất kì trên dantri.com
+ mua một đồ vật yêu thích trên Lazada
+ xem một bộ phim hành động trên phim3s
+ nghe một bản nhạc yêu thích trên nhaccuatui
+ đọc một bài báo trên vnexpress
+ ...

Những tác vụ này đều được ghi lại, cụ thể hơn là trên máy chủ của website mà người dùng vừa truy cập và thực hiện 1 hoặc nhiều tác vụ được kể nêu trên (tất nhiên là còn rất nhiều tác vụ khác). Người làm data mining có thể thu thập lại và khai thác những dữ liệu này để phân tích qua đó có thể tối ưu trải nghiệm của website và phục vụ người dùng tốt hơn. Những tác vụ này được chia thành 2 loại là implicit và explicit.

**Explicit rating, theo nghĩa đen của nó tức là những tác vụ của người dùng đem lại dữ liệu một cách trực tiếp cho người muốn thu thập dữ liệu**. Một ví dụ là nút like và dislike trên các mạng xã hội, các trang chia sẻ video trực tuyến, nghe nhạc như Facebook, Youtube, Pandora, ... hay hệ thống vote theo thang điểm (1,2,3,4 hay 5 sao). Khi người dùng click like, dislike hay vote cho các nội dung mà họ xem, những dữ liệu này có thể được dùng trực tiếp để đánh giá về thói quen hay nhu cầu của họ, giúp hệ thống hiểu người dùng hơn và phục vụ họ tốt hơn bằng cách gợi ý những nội dung có liên quan.

**Implicit rating, cũng theo nghĩa đen của nó tức là những tác vụ mà người dùng thực hiện trên các website nhưng không trực tiếp yêu cầu họ phải đánh giá hay làm gì đó lên nội dung mà họ vừa xem**. Nói cách khác là chúng ta chỉ quan sát xem user làm gì mà thôi. Một vài ví dụ như:

+ Anh A khi vào vnexpress thì chỉ xem 2 mục là Giải trí và Thể thao
+ Chị B đọc tất cả các bài viết về cách giảm cân hiệu quả
+ Chú C mua vài món đồ
+ Cô D luôn tìm đọc những cuốn sách về chiến tranh
+ ...

Như các bạn có thể thấy là hệ thống không yêu cầu người dùng phải tác động gì lên nội dung, mà chỉ quan sát thói quen họ hay làm gì trên website, sau một thời gian sẽ đưa ra được một profile của người dùng và qua đó xây dựng hệ thống tốt hơn để phục vụ họ.

#### Nhược điểm

Implicit và Explicit rating đều có nhược điểm riêng trong data mining mà nếu không khai thác và sử dụng cẩn thận có thể dẫn đến việc phát triển sai thuật toán và gây tác dụng ngược lên trải nghiệm của người dùng.

a. _Explicit rating_

+ Người dùng thường rất lười: khi người dùng xem xong một bản nhạc hay, mua một món đồ ưa thích, hay đọc một cuốn sách, chúng ta thường mong chờ họ đánh giá xem nội dung này thế nào đối với họ để có thể phát triển thuật toán phục vụ họ tốt hơn. Nhưng đừng mong họ làm thế, ít nhất là với số lượng lớn người dùng internet.

+ Người dùng sẽ đưa ra thông tin đánh giá sai lệch: nếu họ có chịu khó một chút để đánh giá về nội dung mà họ vừa xem thì có thể họ sẽ chỉ làm cho có hoặc đánh giá sai, không đúng với cảm nhận của họ về nội dung vừa xem

+ Người dùng thường không quay lại để update những đánh giá họ đã làm trước đó: sở thích có thể thay đổi theo thời gian. Một người thích một ban nhạc nhưng sau đó có thể họ sẽ không thích ban nhạc đó nữa. Giả sử trong quá khứ người đó luôn vote cho những bài hát của ban nhạc Bức Tường. Nhưng sau này anh ta chỉ thích nghe nhạc của Mỹ Tâm, thì chắc chắn là anh ta cũng chẳng bao giờ quay lại website nhạc kia để update những vote đã thực hiện cho Bức Tường.

b. _Implicit rating_

Nhược điểm lớn nhất của implicit rating là thông tin của người dùng đôi lúc hoàn toàn sai lệch:

+ Cô A mua vài món đồ trên Amazon không hẳn là cô ta cần hoặc thích nó. Mà có thể mua hộ ai đó hoặc làm quà cho sinh nhật của cháu gái

+ Anh B và chị C thích 2 thể loại phim khác nhau nhưng lại dùng chung 1 account để download phim trên viettorrent. Anh B dùng thì download phim hành động. Chị C dùng thì download phim hài hước, tình cảm. Như vậy không thể dùng dữ liệu thu thập của account đó để gợi ý phim cho họ. Giả sử lúc chị C dùng account để tìm phim mà toàn nhận được gợi ý là Avatar, Die Hard, James Bond thì chắc là không hài lòng lắm.

Như vậy việc đưa ra thuật toán phân tích dữ liệu thô được thu thập từ tác vụ của người dùng trên hệ thống không hề dễ dàng và cần phải được đánh giá và xem xét một cách rất cẩn thận bởi các nhà phân tích dữ liệu và developer trước khi xây dựng hệ thống phục vụ người dùng.