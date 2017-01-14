---
layout: post
title: Understanding Convolutional Neural Networks (A Beginner's Guide)
date:  2017-01-11 12:54:47
excerpt: "In the future I will be using ConvNets to search for textual patterns and before digging into this work I would like to just create a short introduction on the topic"
mathjax: true
comments: true
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
 <script type="text/x-mathjax-config">
      MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});
    </script>
    <script type="text/javascript" async
      src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_CHTML">
    </script>
Convolutional neural networks have had a lot of buzz in recent years. As the name implies it is a weird combination of biology ,maths and a little CS sprinkled in, but these networks have been some of the most influential innovations in the field of computer vision. 2012 was the first year that neural nets grew to prominence as Alex Krizhevsky used them to win that year’s ImageNet competition (basically, the annual Olympics of computer vision), dropping the classification error record from 26% to 15%, an astounding improvement at the time. Ever since then, a host of companies have been using deep learning at the core of their services. Facebook uses neural nets for their automatic tagging algorithms, Google for their photo search, Amazon for their product recommendations, Pinterest for their home feed personalization, and Instagram for their search infrastructure.<cite>[ A Beginners Guide to Understanding Convolutional Neural Networks][2]</cite>

![alt text](https://adeshpande3.github.io/assets/Cover.png "Illustration of convolutional nets")

Convolutional networks convolutional (LeCun, 1989), also known as neural networks or CNNs, are a specialized kind of neural network for processing data that has a known, grid-like topology. Examples include time-series data, which can be thought of as a 1D grid taking samples at regular time intervals, and image data, which can be thought of as a 2D grid of pixels. Convolutional networks have been tremendously successful in practical applications. The name “convolutional neural
network” indicates that the network employs a mathematical operation called convolution. Convolution is a specialized kind of linear operation. Convolutional networks are simply neural networks that use convolution in place of general matrix multiplication in at least one of their layers.<cite>[ Deep Learning, Ian Goodfellow, Yoshua Bengio, and Aaron Courville][1]</cite>

###The Convolution Operation

I remember from one of my Digital Signal Processing Courses back in the stone age that convolution was used to discretize analog signals. My simple analogy to this operation is that it as a weighted avarage sample of the signal over some time steps. For example

<div>$\sum_{\forall i}{x_i^{2}}$</div>

[1]:http://www.deeplearningbook.org
[2]:https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner's-Guide-To-Understanding-Convolutional-Neural-Networks-Part-2/

## References
1. Deep Learning, 2016, Ian Goodfellow, Yoshua Bengio, and Aaron Courville, Book in preparation for MIT Press
2. A Beginners Guide to Understanding Convolutional Neural Networks, https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner's-Guide-To-Understanding-Convolutional-Neural-Networks-Part-2/





