---
layout: post
title: "Monty Hall problem"
date: 2016-05-17 11:33:20 +0700
categories: statistics
tags: statistics monty_hall
---

This is a very famous probability puzzle. It's based on the American television game show **Let's Make Deal** and not surprisingly the name **Monty Hall** was the game show's host name. Following is a variation of the problem definition:

```
At a game show, master of ceremonies (MC) hides a prize (say 100,000 AU$) behind one of three doors and two 
girls behind the two remaining doors. The contestant picks one of three doors, and then MC opens one of the 
two remaining doors. The contestant is then given the choice to either switch to the remaining door or keep 
the first one that he/she did choose. What should he/she do to win 100,000 AU$?
```
<br>

#### Answer

The contestant **should switch to the remaining door** to maximize his chance of winning the prize.
<br><br>

#### Explanation

First, there are 3 doors and the contestant is allowed to pick 1 door, so the probability that he will get the prize is 1/3 or 33.33%, and the probability that he will not get the prize is 2/3 or 66.67%. In other word, there are 66.67% probabilities the prize will lie behind the 2 doors which were not selected by the contestant:

![Monty Hall problem 1](https://raw.githubusercontent.com/hoanvu/hoanvu.github.io/master/images/posts/monty_hall_1.JPG)
<br><br>

After the MC opens 1 of the 2 remaining doors, which I assume there is a girl behind that door. What happen now is that the last remaining door will get all the 66.67% probabilities for the prize to be behind it: 

![Monty Hall problem 2](https://raw.githubusercontent.com/hoanvu/hoanvu.github.io/master/images/posts/monty_hall_2.JPG)
<br><br>

Now the contestant is given a chance to change his mind:

- If the contestant keeps his original choice, the probability that he will get the prize does not change, which is still 33.33%.

    ![Monty Hall problem 3.1](https://raw.githubusercontent.com/hoanvu/hoanvu.github.io/master/images/posts/monty_hall_3_1.JPG)

- If the contestant switches to the remaining door, his probability will be increased from 33.33% to 66.67%. This is because with one of the door opened, all 66.67% probability will be transferred to the remaining door that was not chosen by the contestant:

    ![Monty Hall problem 3.2](https://raw.githubusercontent.com/hoanvu/hoanvu.github.io/master/images/posts/monty_hall_3_2.JPG)

<br>

In conclusion, **by switching to the remaining door, the contestant will not be guaranteed to win the prize, but his probability to win will be doubled, from 33.33% originally to 66.67%.**
