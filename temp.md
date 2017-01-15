---
layout: post
title: Understanding Convolutional Neural Networks (A Beginner's Guide)
date:  2017-01-11 12:54:47
excerpt: "In the future I will be using ConvNets to search for textual patterns and before digging into this work I would like to just create a short introduction on the topic"
mathjax: true
comments: true
---

Convolutional neural networks have had a lot of buzz in recent years. As the name implies it is a weird combination of biology ,maths and a little CS sprinkled in, but these networks have been some of the most influential innovations in the field of computer vision. 2012 was the first year that neural nets grew to prominence as Alex Krizhevsky used them to win that year’s ImageNet competition (basically, the annual Olympics of computer vision), dropping the classification error record from 26% to 15%, an astounding improvement at the time. Ever since then, a host of companies have been using deep learning at the core of their services. Facebook uses neural nets for their automatic tagging algorithms, Google for their photo search, Amazon for their product recommendations, Pinterest for their home feed personalization, and Instagram for their search infrastructure.<cite>[ A Beginners Guide to Understanding Convolutional Neural Networks][2]</cite>

![alt text](https://adeshpande3.github.io/assets/Cover.png "Illustration of convolutional nets")

Convolutional networks convolutional (LeCun, 1989), also known as neural networks or CNNs, are a specialized kind of neural network for processing data that has a known, grid-like topology. Examples include time-series data, which can be thought of as a 1D grid taking samples at regular time intervals, and image data, which can be thought of as a 2D grid of pixels. Convolutional networks have been tremendously successful in practical applications. The name “convolutional neural
network” indicates that the network employs a mathematical operation called convolution. Convolution is a specialized kind of linear operation. Convolutional networks are simply neural networks that use convolution in place of general matrix multiplication in at least one of their layers.<cite>[ Deep Learning, Ian Goodfellow, Yoshua Bengio, and Aaron Courville][1]</cite>

###The Convolution Operation

I remember from one of my Digital Signal Processing Courses back in the stone age that convolution was used to discretize analog signals. My simple analogy to this operation is that it as a weighted avarage sample of the signal over some time steps, we do this do cancel out noise and to get a more stable signal.

![alt text](http://www.sciweavers.org/download/Tex2Img_1484476324.jpg "Equation convolution")

, where w is a probability density function, x is our signal , t is a time index that can take only integer values and a the number of timesteps with want to average over

The convolution operation is typically denoted like this (with an asterix):

![alt text](http://www.sciweavers.org/download/Tex2Img_1484476520.jpg "Normal notation")

and discrete convolution is typically defined as this: 

![alt text](http://www.sciweavers.org/download/Tex2Img_1484476979.jpg "Discrete notation")

In machine learning applications the input is typically a multidimensional array (does not have to be) of data and the kernel/filter (w(t-a)) are typically an array of parameters that are learned by a ConvNet. The mulitdimensional arrays are usually called tensors.

Typically we convolute over more than one axis at the time (example a 2D image): 

![alt text](http://www.sciweavers.org/download/Tex2Img_1484479920.jpg "Cross correlation")

Convolution is not the only part of ConvNets and usually other operations are calculated at the same time.

Following is a simple visual example of the convolutional operation above. Imagine that the matrix on the left represents an black and white image. Each entry corresponds to one pixel, 0 for black and 1 for white (typically it’s between 0 and 255 for grayscale images). The sliding window is called a kernel, filter, or feature detector. Here we use a 3×3 filter, multiply its values element-wise with the original matrix, then sum them up. To get the full convolution we do this for each element by sliding the filter over the whole matrix.<cite>[ Understanding convolutional neural nets][3]</cite>

![alt text](http://deeplearning.stanford.edu/wiki/images/6/6c/Convolution_schematic.gif "Illustration of convolutional operation")

Source: http://deeplearning.stanford.edu/wiki/images

The parameters of the kernels or filters are typically trained by the network but you have to initilize the values of the parameters. Also typically using Deep Learning tools such as Tensor Flow, one has to specify these how many kernels you want to train for the model. The more kernels the more parameter training. 

The output of the kernels are typically called feature maps. Below is an example of an image that has been blured by using a filter/kernel:

![alt text](http://docs.gimp.org/en/images/filters/examples/generic-taj-convmatrix-blur.jpg "Bluring operation on an image")

Source: http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/

###CNNs

CNNs are basically just several layers of convolutions with nonlinear activation functions like ReLU or tanh applied to the results. These functions are used to capture non-linearity and especially the ReLUslend themselves nicely to the derivation operation used in back-propagation in Neural Networks.  
In a typical feedforward neural network we connect each input neuron to each output neuron in the next layer. This is called a fully connected layer. However, by conducting the convolution operation over the input we get so called sparse connectivity, meaning that not all inputs are connected to a neuron in the next layer. Each layer applies different filters, typically hundreds or thousands like the ones showed above, and combines their results.

![alt text](http://pubs.sciepub.com/ajme/2/7/9/image/fig2.png)

In a traditional feedforward neural network we connect each input neuron to each output neuron in the next layer. That’s also called a fully connected layer, or affine layer. In CNNs we don’t do that. Instead, we use convolutions over the input layer to compute the output. This results in local connections, where each region of the input is connected to a neuron in the output. Each layer applies different filters, typically hundreds or thousands like the ones showed above, and combines their results. There’s also something something called pooling (subsampling) layers, but I’ll get into that later. During the training phase, a CNN automatically learns the values of its filters based on the task you want to perform. For example, in Image Classification a CNN may learn to detect edges from raw pixels in the first layer, then use the edges to detect simple shapes in the second layer, and then use these shapes to deter higher-level features, such as facial shapes in higher layers. The last layer is then a classifier that uses these high-level features.


[1]:http://www.deeplearningbook.org
[2]:https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner's-Guide-To-Understanding-Convolutional-Neural-Networks-Part-2/
[3]:http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/

## References
1. Deep Learning, 2016, Ian Goodfellow, Yoshua Bengio, and Aaron Courville, Book in preparation for MIT Press
2. A Beginners Guide to Understanding Convolutional Neural Networks, https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner's-Guide-To-Understanding-Convolutional-Neural-Networks-Part-2/
3. Understanding convolutional neural networks for NLP, https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner's-Guide-To-Understanding-Convolutional-Neural-Networks-Part-2/





