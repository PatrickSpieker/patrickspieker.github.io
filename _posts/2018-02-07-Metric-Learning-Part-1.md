---
layout: post
title:  "Metric Learning - Part 1: Motivation"
date:   2018-05-21 12:35:52 -0800
---
Note: this is part of my series on metric learning, a technique for learning distance metrics that out perform the 
vanilla Euclidean distance metric. 

## Motivation ##

Suppose we would like to run the _k_-nearest neighbors (k-nn) classification algorithm. k-nn is a non-parametric method
which takes data _n_ points of _m_ dimension and a distance function _d(x,y)_ as input. Given some new _m_-dimensional 
vector _q_,
_k_-nn classifies the point based on the votes of the closest _k_ points to _q_ according to our distance metric _d_. 

If we let our distance metric be the Euclidean distance between the 2 points, we must normalize our features (for some 
reason?) Yeah. Apparently a thing. come back here and briefly discuss

Obviously, though, there are other distance metrics than just the Euclidean. The Mahalanobis distance, for example,
is a slightly different take on distance. It measures the distance between a point and a distribution (i.e. a set of 
points). The mean of the set of points is mu. 


