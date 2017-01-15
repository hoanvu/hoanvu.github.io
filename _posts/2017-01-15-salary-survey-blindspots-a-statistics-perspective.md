---
layout: post
title: "Salary Survey & Blindspots - A statistics perspective"
date: 2017-01-15 10:20:00 +0700
categories: statistics
tags: salary_survey statistics 
---

There was an article on VNExpress (one of the largest Vietnam's news website) about IT industry's salary survey in 2016. It was shared by many friends of mine and quickly became the topic for debates and discussions. People working in IT industry said numbers in the post are hard to believe, but non-IT employees showed lots of admirations about the dream salary reported.

The original link is not available anymore, but you can read [a copy here](http://ndh.vn/luong-nhan-su-it-binh-quan-26-trieu-dong-moi-thang-20170111012737956p125c135.news){:target="_blank"}. 

I read the article and thought that the information mentioned in that salary survey was indeed quite exaggerated, and I was not alone, many others shared the same opinion. And seems to be true, the article was deleted from the website several days later.

In this blog post, I won't stand as an IT guy who deny or approve the truthfulness mentioned by VNExpress because they deleted the news anyway, but as a beginner trying to analyze things using statistics. I'll try to investigate, give some hypothesis and point out flaws that these survey used to have, which in turn failed to convey correct information to readers. As you will see, there're many lurking variables (blindspots) that makes a research like this go wrong.

Basically, there are few steps involved in a study like this:

1. Study design
2. Sampling (or collecting data in simple terms)
3. Exploratory Data Analysis
4. Use probability on sampling data to inference about the population

**The second step is what I'll focus on because data is the most likely the most important component in any statistics research. Without quality data, anything can go wrong.** But other steps will also be discussed briefly.

<br>

#### Study design
There are several types of study:

* Observational study
    1. Prospective observational study
    2. Retrospectice observational study
* Experiment
* Survey

Even if you don't know statistics, you know what type of study it is, ***"Salary survey"***, the name already described everything. The study design will also include analysis for collecting necessary sampling data and methods to accomplish that.

<br>

#### Sampling: where fun stuffs come in
In step one, when a surveyor(s) decided to conduct a study on something (salary of people working in IT industry in this case), they will have to narrow down what's the population to work on. In statistics, population can be descibed as a collection of all similar objects/items/events that a research or study must consider. In this study, the population are all employees working in IT industry. 

Ideally, to get the best result, a study must collect data from each and every object in the population. But in fact, this's almost impossible because you will likely never get enough resources to do so. This is when the concept of **sampling data** comes in. The study designer will try to collect data from a subset of the population, called the **sample**. In order for the result to be as accurate as possible, the sample must be representative of the population as much as possible. 

Right at the beginning, the post said *"Salary for people have more than 2 years of working experience in Vietnam IT industry is ..."* but then they also said *"salary and benefit reports from Vietnamworks"*. This means that data collected in this study comes solely from Vietnamworks website (a job posting site) and they use that data to inference about the entire population (all people working in IT industry). From statistics perspective, this's not an ideal sample. It's an obvious and serious flaw that many people didn't notice.

One thing we don't know is that what sample data the surveyor use to create the article. One guess is that the surveyor is a person working inside Vietnamworks and data is taken internally from their database. This's the most possible option because it's a big website so the data will be huge, so the cost for data collection process will be reduced a lot. But to conclude that their data is representative of Vietnamese IT employee, that would be a big mistake. Why?

* First, **obviously not everyone working in IT industry has a Vietnamworks account**, especially for people working in goverment sector. Government workers usually prefer stable jobs, so they rarely consider to switch company, that's why it's quite understandable that they don't have account in a job posting site. This leads to the second point.
* People working in government **always** have lower salary than people working in private sector. This has a huge impact on the result because **if we include these government workers, the mean salary will be much lower** and more acceptable, but I believe it's not the case here.
* Third, Vietnamworks is not the only job posting site in Vietnam, there are tons of them such as CareerBuilder, ITViec, HR2B, MyWork, TimViecNhanh, TimViec24h, ...
* People have tendency to lie about their salaries online. They will try to put higher salary than actual amount they receive in previous employers in order to hope to get better payment while negotiation with recruiter. This will make the mean salary becomes even higher.
* ...

I called above points **blindspots** for readers because normally they can't recognize them while reading a news article on the internet. These surveyor posted many numbers, but they didn't provide what was the sample data or many times the sample data is not a representation of the population targeted by the study like in this case. 

<br>

#### Exploratory Data Analysis
This step uses descriptive statistics to explore hidden features in data. There's also one point I want to discuss that'll impact the information conveyed to reader incorrectly.

People argued that the amount of $800/month is the average salary for the fresher. You will need to understand that when it's about salary, there are many potential outliers. For example, the employer I'm working for pay the amount of minimum $2500/month to a fresher that just completed university, and there are many freshers like that in my company. They are very talented and very rare, so if their salaries were put together with others, this will make the mean salary to become unexpectedly high as reported in the news article. 

One way to eliminate the bias is to use statistical **median** rather than **mean** because mean is affected by outliers and median is not. For example, if you have 5 fresher with respective salaries as below:

* Person 1: $400/month
* Person 2: $450/month
* Person 3: $350/month
* Person 4: $2500/month (outlier)
* Person 5: $500/month

Calculate the mean and median salary for above 5 people, you will see the difference. 

* Mean = $840/month
* Median = $450/month (more realistic)

I think $400/month is the standard salary for a fresher in Vietnam, and as you would see, if the data includes the outlier (Person 4 who's working in my firm), the average salary will raise up to $840/month, which is almost equal to the number reported in the article.

But of course I can't be sure which measurement was used by the surveyor, so can't conclude whether it's sample data issue or surveyor's approach issue.

<br>

#### Inferencing
This step uses sampling data to inference about the population. Which means that if the sampling data contains biases, what was concluded about the population will also be incorrect.

<br>

#### Conclusion
One point to take home for reader is that when you read something related to statistics, read and enjoy it, but don't trust it and waste your time argue with others. Because people can lie very well with statistics. Always question what you're reading.