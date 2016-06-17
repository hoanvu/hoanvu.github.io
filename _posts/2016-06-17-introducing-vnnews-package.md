---
layout: post
title: "Introducing vnnews package"
date: 2016-06-17 11:51:30 +0700
categories: python
tags: python
---

I've had to crawl the web to collect a lot of data for studying machine learning recently. Writing the same code again and again to perform the same task made me decided to write a separate Python package for dealing with this kind of job, and `vnnews` is the result.  

[You can download or clone the repository on GitHub here](https://github.com/hoanvu/vnnews). Documentation is updated frequently for the APIs so you should have no problem getting acquaintance with it.

Right now, the package only has APIs to crawl data from VNExpress.net - a very famous news website in Vietnam. I will try to provide APIs for other websites in the future if there are needs for that. By the time of this writing, also a limited number of news categories are supported, but adding support for new cateogies are easy, so I will try to update them soon. Please visit the repository page for further information.
<br><br>

### Challenges

Crawling a website is both an easy and not easy task. It's easy because once you get hold of the page's DOM, you can get anything out of it. Most high level programming languages have good libraries to help you with this. It's difficult because the page's developer may change their code, so your crawler will be broken, and to understand why it's broken and how to fix it will really take a lot of time and effort. Also different pages in a website may have different DOM structure, so in order to write a good crawler, you will need to take time to understand the website you are crawling.

For VNExpress, there are several types of pages that have different DOM structure than others. Here they are (this may not be an exhaustive list at the time you are reading this):

- A normal news page: [http://vnexpress.net/tin-tuc/the-gioi/tau-cuu-nan-tot-nhat-trung-quoc-tham-gia-tim-may-bay-viet-nam-3421568.html](http://vnexpress.net/tin-tuc/the-gioi/tau-cuu-nan-tot-nhat-trung-quoc-tham-gia-tim-may-bay-viet-nam-3421568.html)
- A live page with images and some texts: [http://vnexpress.net/tin-tuc/thoi-su/dua-manh-vo-may-bay-casa-ve-dat-lien-3421288.html](http://vnexpress.net/tin-tuc/thoi-su/dua-manh-vo-may-bay-casa-ve-dat-lien-3421288.html)
- A live page with images and very few texts: [http://vnexpress.net/tin-tuc/thoi-su/le-don-tong-thong-my-obama-tai-phu-chu-tich-3407393.html](http://vnexpress.net/tin-tuc/thoi-su/le-don-tong-thong-my-obama-tai-phu-chu-tich-3407393.html) 
- An interactive page with only images, no text: [http://vnexpress.net/interactive/2016/ket-qua-bau-cu/](http://vnexpress.net/interactive/2016/ket-qua-bau-cu/)
- An interactive page with images and some texts: [http://vnexpress.net/interactive/2016/dai-bieu-quoc-hoi](http://vnexpress.net/interactive/2016/dai-bieu-quoc-hoi)

It's necessary to write code to handle all these types of DOM structures.
<br><br>

### What's next?

I will try my best to update the APIs so they'll be as exhaustive as possible. If you have any request, please send them to [**my personal email**](mailto:vumaihoan@gmail.com) or create an **Issues** in the repository page on GitHub.  