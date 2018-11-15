---
layout: post
title:  "Afternoon ML  - Part 1: Linear Regression"
date:   2018-02-07 12:35:52 -0800
---
Note: This is a part of my ongoing afternoon post series, in which I take a 
basic (undergrad ML-level) topic, research it, and then write a blog post and
accompanying code for it, all within about 3 hours (an afternoon). 

Today's topic is regression, the implicit model behind all of random Matlab
functions your intro statistics class had you call. Regression is a pretty bedrock
machine learning method, making straight-forward assumptions and with relatively
interpretable parameters. 

Before we get to that, let's motivate why we might use regression with an example.

Possible Motivating examples (need better one):
(1) Suppose we are a graduate school, tasked with deciding which undergraduates we
should admit to our institution. To do this, we look at ou current graduate students,
and consider who is succeeding and who is not. 

(2) Suppose we are a hedge fund, and we are trying to decide whether or not to invest in
a car company by trying to predict how many miles per gallon its latest prototype 
car will have on average. 
We've learned a few pieces of information about the car from various press releases
and rumors - the number of cylindars (3), the number of horsepower (200), and whether
or not the car is certified as "green" by the EPA (it is). We also have a bunch of 
old examples of cars that have been released by this company, *including their 
miles per gallon*. We can arrange these the table below:

 Cylindars | Horsepower | EPA Green? | MPG
--- | --- | --- |
 5 | 400 | No | 25
 3 | 50 | Yes | 29
 4 | 100 | No | 26

##### Assumptions #####
* MPG can be predicted from the inputs of cylinders, horsepower, EPA Green-ness
* 

We call cyliners, horsepower, EPA Green-ness "features", and we stack them into a
vector x s.t. x[0] = cylinders, x[1] = horsepower, x[2] = epa green-ness (0 or 1).

MPG =

References: UW CSE Machine Learning Coursework (Emily's website, Noah's website,
Sham's website).
