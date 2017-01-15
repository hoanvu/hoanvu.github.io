---
layout: post
title: "Using KMeans to cluster 1D data"
date: 2016-05-07 22:23:20 +0700
categories: algorithm data_science
tags: algorithm kmeans unsupervised_learning
---

#### Problem:

```
Given the following set: { 2, 4, 10, 12, 3, 20, 30, 11, 25 }. Write pseudo code for k-means clustering 
algorithm to cluster the above set to 2 clusters. Then implement code to achieve the same.
```

For some of you who didn't already know, the K-means clustering algorithm should not be used to cluster 1D data, but for the sake of explaining the algorithm, we will use it to solve this problem.
<br><br>

#### KMeans definition, according to Wikipedia:

```
k-means clustering is a method of vector quantization, originally from signal processing, that is popular for cluster analysis in data mining. k-means clustering aims to partition n observations into k clusters in which each observation belongs to the cluster with the nearest mean, serving as a prototype of the cluster. This 
results in a partitioning of the data space into Voronoi cells.
```

By reading the definition, k-means from our problem becomes 2-means because we are asked to separate the input set into 2 clusters. To accomplish this, we will also need 2 numbers, or 2 means, each mean will act as the centroid for each cluster. Let's call these two m1 and m2.

Few key things about KMeans: 

+ It's an unsupervised learning algorithm, which mean input data are not labelled in advanced
+ We need to choose how many clusters (or ```k```) that input data will be grouped into
<br><br>

#### Pseudo-code:

```
1. Initiate m1 & m2
2. REPEAT steps 2.1 to 2.3:
   2.1. Calculate the Manhattan distance from each element to 2 centroids (m1 & m2)
   2.2. Assign each element to the nearest centroid based on the Manhattan distance (forming k clusters)
   2.3. Calculate the mean for all items in each cluster and update m1 & m2 accordingly
3. UNTIL the centroids do not change anymore (or very little)
```

**Note**: it's not compulsory that you have to use Manhattan distance. You can use other type of distance calculation like Euclidean. It's perfectly fine.
<br><br>

#### Pseudo-code walkthrough:

**Step 1: Initiate m1 & m2:**

Because we have no clue which numbers to select as centroids to begin with, let's choose the first 2 numbers in the set:

+ m1 = 2
+ m2 = 4

The whole point of K-means clustering is that these centroids will be updated through time, they will not be fixed. After each iteration, members of each cluster will change and therefore affects the value of the cluster's mean.
<br>

**Step 2 - Iteration 1:**

2.1. Calculate the Manhattan distance:

|  Element ---  | --- Distance to m1 (2)--- | --- Distance to m2 (4) 
|  :-------:  |  :------------------: | :------------------: 
|  2           |  0                      | 2                  
|  4           |  2                      | 0                  
|  10          |  8                      | 6                  
|  12          |  10                     | 8                  
|  3            |  1                      | 1                  
|  20          |  18                    | 16                 
|  30            |  28                     | 26                 
|  11            |  9                      | 7                  
|  25           |  23                     | 21         

<br>
2.2. From the above table, we have the following clusters:

```
Cluster_1: {2, 3}
Cluster_2: {4, 10, 12, 20, 30, 11, 25}
```

2.3. Calculate the mean and update m1 & m2:

```
m1 = mean of Cluster_1 = 2.5
m2 = mean of Cluster_2 = 16
```
<br>

**Step 2 - Iteration 2:**

2.1. Calculate the Manhattan distance:

|Element ---| --- Distance to m1 (2.5) ---|  --- Distance to m2 (16)
| :---: | :---:| :---:
|2   |0.5 |14
|4   |1.5 |12
|10  |7.5 |6
|12  |9.5 |4
|3   |0.5 |13
|20  |17.5  |  4
|30  |27.5  |  14
|11  |9.5 |5
|25  |22.5  |  9

<br>
2.2. From the above table, we have the following clusters:

```
Cluster_1: {2, 4, 3}
Cluster_2: {10, 12, 20, 30, 11, 25}
```

2.3. Calculate the mean and update m1 & m2:

```
m1 = mean of Cluster_1 = 4.5
m2 = mean of Cluster_2 = 18
```
<br>

**Step 2 - Iteration 3:**

2.1. Calculate the Manhattan distance:

|Element --- | --- Distance to m1 (4.5) --- | --- Distance to m2 (18)
| :---: | :---:| :---:
|2   |2.5 |16
|4   |0.5 |14
|10  |5.5 |8
|12  |7.5 |6
|3   |1.5 |15
|20  |15.5 |   2
|30  |25.5  |  12
|11  |6.5 |7
|25  |20.5 |   7

<br>
2.2. From the above table, we have the following clusters:

```
Cluster_1: {2, 4, 10, 3, 11}
Cluster_2: {12, 20, 30, 25}
```

2.3. Calculate the mean and update m1 & m2:

```
m1 = mean of Cluster_1 = 6
m2 = mean of Cluster_2 = 21.75
```
<br>

**Step 2 - Iteration 4:**

2.1. Calculate the Manhattan distance:

|Element ---| --- Distance to m1 (6) --- | --- Distance to m2 (21.75)
| :---: | :---:| :---:
|2   |4 |  19.75
|4   |2  | 17.75
|10  |4  | 11.75
|12  |6  | 9.75
|3   |3  | 18.75
|20  |14 | 1.75
|30  |24 | 8.25
|11  |5  | 10.75
|25  |19 | 3.25

<br>
2.2. From the above table, we have the following clusters:

```
Cluster_1: {2, 4, 10, 12, 3, 11}
Cluster_2: {20, 30, 25}
```

2.3. Calculate the mean and update m1 & m2:

```
m1 = mean of Cluster_1 = 7
m2 = mean of Cluster_2 = 25
```
<br>

**Step 2 - Iteration 5:**

2.1. Calculate the Manhattan distance:

|Element --- | --- Distance to m1 (7) --- | ---  Distance to m2 (25)
| :---: | :---:| :---:
|2  | 5  | 23
|4  | 3  | 21
|10 | 3  | 15
|12 | 5  | 13
|3  | 4  | 22
|20 | 13 | 5
|30 | 23 | 5
|11 | 4  | 14
|25 | 18 | 0

<br>
2.2. From the above table, items are clustered as following:

```
Cluster_1: {2, 4, 10, 12, 3, 11}
Cluster_2: {20, 30, 25}
```

2.3. Calculate the mean and update m1 & m2:

```
m1 = mean of Cluster_1 = 7
m2 = mean of Cluster_2 = 25
```

After iteration 5, we observe that m1 and m2 do not change their values, they are still 7 and 25. So we will stop the process and the result is 2 separate clusters:

```
Cluster_1: {2, 4, 10, 12, 3, 11}
Cluster_2: {20, 30, 25}
```

For [full code implementation, you can see here](https://github.com/hoanvu/assignment/blob/master/problem_7_kmeans.py). The implementation use pure Python, without including any external libraries.
<br><br>

#### Conclusion

So by repeating calculating the cluster centroids and re-grouping items in each cluster based on new centroid's values (using distance formulas like Manhattan, Euclidean, ... distance), we are able to cluster input data into correct groups after a number of iterations.

In some later posts, I will introduce ways to evaluate the performance of KMeans algorithm and how to choose suitable ```k``` for your data.