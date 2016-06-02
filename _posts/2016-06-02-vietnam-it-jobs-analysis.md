---
layout: post
title: "Vietnam IT Jobs Analysis"
date: 2016-05-28 10:07:30 +0700
categories: data_mining visualization
tags: data_mining visualization matplotlib pandas
---


### Introduction

I've been looking for a Data Analysis job recently and failed to do so. Actually I got several offers for Python Developer position but the work in these companies are quite boring so I left. The fact is Data Science / Data Mining / Machine Learning jobs in the north of Vietnam are quite rare. There are a lot more jobs in this field in Ho Chi Minh city.

With my free time I decided to do some analysis about job market for the last few months in Vietnam. This is written with the main purpose to consolidate my knowledge about exploratory data analysis, so I will not take it very seriously about data source. I wrote some scripts to crawl job data from only one website Vietnamworks.com for the last few months. I tried to get data for the first 5 months of 2016, but it seems Vietnamworks doesn't show their past data after a specific period. The best I could get is from April. Not much, but this is for fun anyway.

[In my last post](http://hoanvu.github.io/2016/05/scraping-jobs-from-vietnamworks), I showed you how to crawl job data from Vietnamworks using BeautifulSoup. Scripts used in that post will be reused here, but the scope is a little bit wider (from 26 URLs and several other features).

This post will focus on scaping data for IT jobs, but you can change the base URL to work with any other kind of job you want. Just go to Vietnamworks, use the website's filter to select the job categories you want to play with, and get the base URL and assign it to the `base_url` variable in `get_all_urls()` method.

### Package requirements:

If you do not have those packages installed on your system, please do so before continue:

- Python 2.7
- beautifulsoup4
- matplotlib
- seaborn
- pandas 


```python
# Imports & Settings

# Make sure packages in my virtual environment are included
import sys
sys.path.append('/home/hoanvu/anaconda2/envs/ds/lib/python2.7/site-packages/')

import requests
import pickle
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from bs4 import BeautifulSoup
from collections import Counter, defaultdict
from datetime import datetime

%pylab inline
sns.set_context('poster')

# No of URLs to crawl from Vietnamworks
MAX_PAGE = 27
```

    Populating the interactive namespace from numpy and matplotlib


    WARNING: pylab import has clobbered these variables: ['datetime']
    `%matplotlib` prevents importing * from pylab and numpy


Next, we will write a method to get all URLs for the job categories of your choice. 
- base_url: this is the URL of the first page after you configure your filter on Vietnamworks website and press 'Search'
- extended_url_pages: we want to crawl more than just the first page. `base_url` is the first page, all subsequence pages will have the extension in the URL, with `page-2` for the second page, `page-3` for the third page and so on

  We we get advantage of this uniform to construct our list of URLs


```python
def get_all_urls():
    """
    Scan through all URLs defined by MAX_PAGE and return the URL
    
    return: list of URLs
    """
    
    base_url = 'http://www.vietnamworks.com/it-hardware-networking-it-software-jobs-i55,35-en'
    extended_url_pages = ['/page-{}'.format(page_number) for page_number in xrange(2, MAX_PAGE)]
    urls = [base_url + extended_page for extended_page in extended_url_pages]
    urls.insert(0, base_url)
    return urls
```

### Data collection

Features that need to be collect:

- Job title
- Technical skills
- Work location
- Position
- Company name
- Job post date

This method get_jobs_in_url() get details for all job in a single URL. You can see my [previous post](http://127.0.0.1:4000/2016/05/vietnam-it-jobs-analysis) for explanation about the code.


```python
def get_jobs_in_url(url):
    """
    Take a single URL and return a pandas DataFrame contains details about all jobs in that URL.
    
    return: pandas.DataFrame
    """
    req = requests.get(url)
    soup = BeautifulSoup(req.content, 'html.parser')
    
    jobs_table = soup.find('table', {'class': 'link-list'})
    tr_tags = jobs_table.find_all('tr', {'class': 'job-post'})
    
    job_title = []
    job_company = []
    job_location = []
    job_position = []
    job_skills = []
    job_date = []
    
    for job in tr_tags:
        job_title.append(job.find('a', {'class': 'job-title'}).contents[0])
        job_company.append(job.find('span', 'name').contents[0])
        job_location.append(job.find('p', {'class': 'job-info'}).contents[1].find('span').contents[0])
        job_position.append(job.find('p', {'class': 'job-info'}).contents[1].find_all('span')[1].contents[0])
                            
        skill_list_data = job.find('div', {'class': 'skills'})
        if skill_list_data:
            skill_list = skill_list_data.find_all('em', {'class': 'text-clip'})
            
        job_skills.append([skill.contents[0] for skill in skill_list])
        
        # Job post date
        d = job.find('span', {'class': 'views'}).find('span').contents[0].split(' ')[1]
        if d == 'Today':
            d = datetime.datetime.now().strftime("%d/%m/%Y")
        job_date.append(d)
    
        # Job salary
        
    return pd.DataFrame({
            'job_title': job_title,
            'company': job_company,
            'location': job_location,
            'position': job_position,
            'skills': job_skills,
            'post_date': job_date
        })
```

This method `get_all_jobs()` just scan through all URLs from `get_all_urls()` and get details for all jobs listed in each and every page:


```python
def get_all_jobs():
    """
    Scans all URLs and crawls all jobs from all pages
    
    return: pandas.DataFrame contains every possible job that we can find
    """
    urls = get_all_urls()
    data = pd.DataFrame()
    for url in urls:
        data = data.append(get_jobs_in_url(url), ignore_index=True)
        
    return data

jobs = get_all_jobs()
```


```python
# Convert the job post date to datetime type
jobs['post_date'] = pd.to_datetime(jobs.post_date, format="%d/%m/%Y")
```

#### Let's take a quick look at our data:


```python
jobs.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>company</th>
      <th>job_title</th>
      <th>location</th>
      <th>position</th>
      <th>post_date</th>
      <th>skills</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Công Ty Cổ Phần Sabre Việt Nam</td>
      <td>Chuyên Viên IT</td>
      <td>Ha Noi</td>
      <td>Experienced (non-manager)</td>
      <td>2016-06-02</td>
      <td>[Máy Tính, Mạng, Triển Khai Tổng Đài IP]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Công Ty TNHH Vận Hành Jmango Việt Nam</td>
      <td>Java Developer (quantity: 3)</td>
      <td>Ha Noi</td>
      <td>Experienced (non-manager)</td>
      <td>2016-05-26</td>
      <td>[SQL Server-mysql, HTML - CSS - Javascript, Ja...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CSC Vietnam</td>
      <td>SAP Consultants (real Estate, Fi, Co, Ps, Mm, ...</td>
      <td>Ho Chi Minh</td>
      <td>Experienced (non-manager)</td>
      <td>2016-05-25</td>
      <td>[SAP &amp; ERP, SAP Consultant ( FI / CO/ MM ) - R...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CSC Vietnam</td>
      <td>Senior Software Engineer (with Japanese Language)</td>
      <td>Ho Chi Minh</td>
      <td>Experienced (non-manager)</td>
      <td>2016-05-18</td>
      <td>[Interpreter - Translator, Bridge Engineer ( J...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CSC Vietnam</td>
      <td>Java Senior Software Engineer</td>
      <td>Ho Chi Minh</td>
      <td>Experienced (non-manager)</td>
      <td>2016-05-18</td>
      <td>[J2EE Architecture, Java Developer - IT Softwa...</td>
    </tr>
  </tbody>
</table>
</div>


<br>
Nice, seems that our data is not very **clean**, but it says that our code until now is working. Now, let's jump to the most interesting part and see what our data says?

### Exploratory Data Analysis

At first I planned to clean this dataset a little bit more, but then I realize it would be better if I keep it this way and transform each column based on the information I need. If you read this, feel free to take the dataset and tweak it the way you want.

We will try to answer few questions as we go. 
<br><br>

#### First, what is the general status of Vietnam job market?

How many days did we collect the data?


```python
print jobs.post_date.max() - jobs.post_date.min()
```

    37 days 00:00:00


How many jobs were posted during this period?


```python
print "Total jobs: {}".format(len(jobs))
```

    Total jobs: 1279


**1277 jobs** were posted in **only 37 days**, I think that this is very interesting number to show that the Vietnam job market is **very bustle**. If we collect data from other sites, there maybe even much bigger number of jobs posted.
<br><br>

#### Which city have the most demand for job recruitment?

From the graph below, it's obvious that **Ho Chi Minh** and **Ha Noi** are two cities which have huge demand for human resources in IT, which makes sense! Ho Chi Minh is by far the most demanding city.

**Da Nang** is also a very hot city for job hunter. There are some jobs that have work location as **International**, this is very interesting!


```python
all_locations = []
for location in jobs.location:
    if ',' in location:
        all_locations.extend(location.split(', '))
    else:
        all_locations.append(location)

# Remove cities that have less than 5 jobs, just to make grap clearer
most_cities = [key for key, value in Counter(all_locations).iteritems() if value > 5]
new_cities = [city for city in all_locations if city in most_cities]

sns.countplot(y=new_cities)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7fb35e016ad0>




![png](https://github.com/hoanvu/hoanvu.github.io/blob/master/images/posts/jobs_by_city.png?raw=true)
<br><br>

#### What's the percentage?


```python
from __future__ import division

location_counter = Counter(all_locations)
total_jobs = sum(location_counter.values())
jobs_in_hcm = location_counter['Ho Chi Minh']
jobs_in_hn = location_counter['Ha Noi']
jobs_in_dn = location_counter['Da Nang']
jobs_in_int = location_counter['International']

print "Total jobs:                     {}".format(total_jobs)
print "Jobs required by Ho Chi Minh:   {:.3f}%".format((jobs_in_hcm / total_jobs) * 100.0 )
print "Jobs required by Ha Noi:        {:.3f}%".format((jobs_in_hn / total_jobs) * 100.0 ) 
print "Jobs required by Da Nang:       {:.3f}%".format((jobs_in_dn / total_jobs) * 100.0 )
print "Jobs required by International: {:.3f}%".format((jobs_in_int / total_jobs) * 100.0) 
```

    Total jobs:                     1477
    Jobs required by Ho Chi Minh:   52.200%
    Jobs required by Ha Noi:        35.003%
    Jobs required by Da Nang:       3.927%
    Jobs required by International: 2.370%
    
<br>

#### Which positions does recruiter looking for?


```python
sns.countplot(x='position', data=jobs)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7fb35e016290>




![png](https://github.com/hoanvu/hoanvu.github.io/blob/master/images/posts/jobs_by_position.png?raw=true)


It's obvious that **Specialist** position is the hottest job. 
<br><br>

#### Now, which skills are expected by companies?


```python
# Need to improve this code

skill_counter = defaultdict(int)
for row in jobs.skills:
    for skill in row:
        skill = skill.lower()
        if 'c++' in skill:
            skill_counter['C++'] += 1
        if 'java' in skill or 'j2ee' in skill or 'servlet' in skill or 'jsp' in skill or 'hibernate' in skill:
            skill_counter['Java'] += 1
        if 'ios' in skill or 'objective-c' in skill or 'objective c' in skill:
            skill_counter['iOS'] += 1
        if 'python' in skill or 'django' in skill or 'flask' in skill:
            skill_counter['Python'] += 1
        if 'html' in skill or 'css' in skill or 'css3' in skill:
            skill_counter['HTML/CSS'] += 1
        if 'android' in skill:
            skill_counter['Android'] += 1
        if 'oracle' in skill or 'sql' in skill or 'sql server' in skill or 'mysql' in skill or \
            'database' in skill or 'postgres' in skill:
            skill_counter['Database'] += 1
        if 'linux' in skill or 'redhat' in skill or 'centos' in skill or 'ubuntu' in skill:
            skill_counter['Linux'] += 1
        if 'cisco' in skill or 'ccna' in skill or 'ccnp' in skill or 'ccie' in skill or \
            'network' in skill or 'routing' in skill or 'switching' in skill:
            skill_counter['Network'] += 1
        if 'c#' in skill or '.net' in skill:
            skill_counter['C#/.Net'] += 1
        if 'javascript' in skill:
            skill_counter['Javascript'] += 1
        if 'php' in skill:
            skill_counter['PHP'] += 1
        if 'scrum' in skill:
            skill_counter['Agile Scrum'] += 1
        if 'brse' in skill or 'bridge' in skill:
            skill_counter['BrSE'] += 1

skills = pd.DataFrame(dict(skill_counter), index=range(1))
skills.iloc[0].sort_values(ascending=False).plot(kind='barh')
# sns.barplot(data=pd.DataFrame(dict(skill_counter), index=range(1)), orient='h')
# sns.barplot?
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7fb35bb182d0>




![png](https://github.com/hoanvu/hoanvu.github.io/blob/master/images/posts/jobs_by_skill.png?raw=true)


This might not be 100% percent accurate, but skill, we know that Java is always the dominated programming language for a very long time.
<br><br>

#### Which companies are hiring people to work outside Vietnam?


```python
jobs[jobs.location.str.contains('International')][['company', 'job_title']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>company</th>
      <th>job_title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>Gmo-z.com Vietnam Lab Center</td>
      <td>Kỹ Sư Phần Mềm Biết Tiếng Nhật (bse/ Smartphon...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Saritasa</td>
      <td>Senior iOS Mobile Developer - Competitive Salary</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Harvey Nash Viet Nam</td>
      <td>Senior Sharepoint Developer (go Onsite Singapore)</td>
    </tr>
    <tr>
      <th>111</th>
      <td>Robert Bosch Engineering Vietnam</td>
      <td>*urgent* 3 Senior Liferay Engineers (4 - 6 Years)</td>
    </tr>
    <tr>
      <th>170</th>
      <td>Công Ty TNHH Thương Mại Và Dịch Vụ Tri Thức Mới</td>
      <td>[tuyển Gấp] 8 Lập Trình Viên .NET, Php, Java C...</td>
    </tr>
    <tr>
      <th>178</th>
      <td>Công Ty TNHH Phần Mềm FPT</td>
      <td>Kỹ Sư Cầu Nối (BrSE) Làm Việc Dài Hạn Tại Nhật...</td>
    </tr>
    <tr>
      <th>211</th>
      <td>Neos Corporation</td>
      <td>Web Developer - Làm Việc Tại Nhật Bản</td>
    </tr>
    <tr>
      <th>268</th>
      <td>Công Ty TNHH Phần Mềm FPT (FPT Software)</td>
      <td>10 Testers Tiếng Nhật N2 Có Cơ Hội Onsite Mỹ</td>
    </tr>
    <tr>
      <th>305</th>
      <td>Neos Corporation</td>
      <td>05 Kỹ Sư iOS ( High Salary )</td>
    </tr>
    <tr>
      <th>306</th>
      <td>Neos Corporation</td>
      <td>05 Kỹ Sư Android ( High Salary )</td>
    </tr>
    <tr>
      <th>341</th>
      <td>CSC Vietnam</td>
      <td>Scrum Master for iOS (onsite Dubai)</td>
    </tr>
    <tr>
      <th>460</th>
      <td>Synova Solutions</td>
      <td>Urgent - PHP Developer (drupal/wordpress/symfo...</td>
    </tr>
    <tr>
      <th>620</th>
      <td>Công Ty TNHH Công Nghệ Phần Mềm Kaopiz</td>
      <td>Onsite Engineer</td>
    </tr>
    <tr>
      <th>628</th>
      <td>Tổng Công Ty Cổ Phần Bảo Hiểm Sài Gòn - Hà Nội...</td>
      <td>Chuyên Viên Công Nghệ Thông Tin ( Làm Việc Tại...</td>
    </tr>
    <tr>
      <th>664</th>
      <td>Công Ty Phần Mềm Của Nhật Bản</td>
      <td>Kỹ Sư Hệ Thống Biết Tiếng Nhật (BrSE)</td>
    </tr>
    <tr>
      <th>698</th>
      <td>Neos Corporation</td>
      <td>03 Bridge System Engineer ( $1000 ~ $2000)</td>
    </tr>
    <tr>
      <th>704</th>
      <td>Imaginato</td>
      <td>($700 ~$1500) E-commerce PHP Engineer</td>
    </tr>
    <tr>
      <th>711</th>
      <td>Finexus Sdn Bhd</td>
      <td>*** Hot :15 Lập Trình Viên Java Làm Việc Tại M...</td>
    </tr>
    <tr>
      <th>724</th>
      <td>Sutherland Global Services Malaysia</td>
      <td>Technical Support</td>
    </tr>
    <tr>
      <th>728</th>
      <td>株式会社プロフェースシステムズ</td>
      <td>System Engineer To Japan ($2000 ~ $5000)</td>
    </tr>
    <tr>
      <th>847</th>
      <td>Marketjs</td>
      <td>Game Developer ( Mobile / Web / Programmer / H...</td>
    </tr>
    <tr>
      <th>862</th>
      <td>Công Ty TNHH Thương Mại Toàn Cầu</td>
      <td>[$2100 - $4000] BSE . Cầu Nối Kỹ Sư Việt - Nhật</td>
    </tr>
    <tr>
      <th>864</th>
      <td>Lucky Ruby Casino &amp; Resort</td>
      <td>System Programmer</td>
    </tr>
    <tr>
      <th>885</th>
      <td>COMIT Corporation</td>
      <td>Kỹ Sư Tối Ưu Hóa Mạng Vô Tuyến 3G (Experienced...</td>
    </tr>
    <tr>
      <th>895</th>
      <td>Synova Solutions</td>
      <td>Urgent - Senior Frontend Developer (location: ...</td>
    </tr>
    <tr>
      <th>949</th>
      <td>Iprice Group</td>
      <td>Senior Software Engineer</td>
    </tr>
    <tr>
      <th>962</th>
      <td>Paxcreation</td>
      <td>Senior PHP Developer (exp 3+ Years) - Up To 10...</td>
    </tr>
    <tr>
      <th>993</th>
      <td>The Database Consultants, LLC</td>
      <td>SharePoint Developer/admin To Work in Hawaii, USA</td>
    </tr>
    <tr>
      <th>995</th>
      <td>ZTE Corporation</td>
      <td>Oversea Project Manager ( Working in Peru )- U...</td>
    </tr>
    <tr>
      <th>1023</th>
      <td>Công Ty Cổ Phần Phát Triển Nguồn Nhân Lực Quốc...</td>
      <td>Kỹ Sư Công Nghệ Thông Tin (Làm Việc Tại Nhật Bản)</td>
    </tr>
    <tr>
      <th>1062</th>
      <td>Saritasa</td>
      <td>Senior Angularjs Javascript (js) Developer - C...</td>
    </tr>
    <tr>
      <th>1106</th>
      <td>Onea</td>
      <td>JAVA Developer</td>
    </tr>
    <tr>
      <th>1219</th>
      <td>Finexus Sdn Bhd</td>
      <td>10 Lập Trình Viên Java (sắp Tốt Nghiệp - 3 Năm...</td>
    </tr>
    <tr>
      <th>1229</th>
      <td>Ars Nova Viet Nam Company Limited</td>
      <td>Kỹ Sư Phần Mềm Được Đào Tạo Tiếng Nhật và Sẽ L...</td>
    </tr>
    <tr>
      <th>1254</th>
      <td>Rivercrane Viet Nam</td>
      <td>PHP Developer (High Salary!)</td>
    </tr>
  </tbody>
</table>
</div>

<br>

####  Have fun!