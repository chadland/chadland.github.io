---
layout: post
title: Understanding Convolutional Neural Networks (A High Level Introduction)
date:  2017-01-11 12:54:47
excerpt: "In the future I will be using ConvNets to search for textual patterns and prior to digging into this work I would like to create a very high level intro on the topic"
mathjax: true
comments: true
---

Convolutional neural networks have had a lot of buzz in recent years. As the name implies it is a weird combination of biology, maths and a little CS sprinkled in, but these networks have been some of the most influential innovations in the field of computer vision. 2012 was the first year that neural nets grew to prominence as Alex Krizhevsky used them to win that year’s ImageNet competition (basically, the annual Olympics of computer vision), dropping the classification error record from 26% to 15%, an astounding improvement at the time. Ever since then, a host of companies have been using deep learning at the core of their services. Facebook uses neural nets for their automatic tagging algorithms, Google for their photo search, Amazon for their product recommendations, Pinterest for their home feed personalization, and Instagram for their search infrastructure. <cite>[ A Beginners Guide to Understanding Convolutional Neural Networks][2]</cite>

![alt text](https://adeshpande3.github.io/assets/Cover.png "Illustration of convolutional nets")

Convolutional networks (LeCun, 1989), also known as neural networks or CNNs, are a specialized kind of neural network for processing data that has a known, grid-like topology. Examples include time-series data, which can be thought of as a 1D grid taking samples at regular time intervals, and image data, which can be thought of as a 2D grid of pixels. Convolutional networks have been tremendously successful in practical applications. The name “convolutional neural
network” indicates that the network employs a mathematical operation called convolution. Convolution is a specialized kind of linear operation. Convolutional networks are simply neural networks that use convolution in place of general matrix multiplication in at least one of their layers. <cite>[ Deep Learning, Ian Goodfellow, Yoshua Bengio, and Aaron Courville][1]</cite>

###The Convolution Operation

I remember from one of my Digital Signal Processing Courses back in the stone age that convolution was used to discretize analog signals. My simple analogy to this operation is a weighted average sample of the signal over some time steps, we did this to cancel out noise and to get a more stable signal.

![alt text](http://www.sciweavers.org/download/Tex2Img_1484476324.jpg "Equation convolution")

, where w is a probability density function, x is our signal, t is a time index that can take only integer values and a the number of time steps we want to average over

The convolution operation is typically denoted like this (with an asterix):

![alt text](http://www.sciweavers.org/download/Tex2Img_1484476520.jpg "Normal notation")

and discrete convolution is typically defined as this: 

![alt text](http://www.sciweavers.org/download/Tex2Img_1484476979.jpg "Discrete notation")

In machine learning applications the input is typically a multidimensional array (does not have to be) of data and the kernel/filter (w(t-a)) are typically an array of parameters that are learned. The multidimensional arrays are usually called tensors.

Typically, we convolute over more than one axis at the time (example a 2D image): 

![alt text](http://www.sciweavers.org/download/Tex2Img_1484479920.jpg "Cross correlation")

Convolution is not the only part of ConvNets and usually other operations are calculated at the same time.

Following is a simple visual example of the convolutional operation above. Imagine that the matrix on the left represents an black and white image. Each entry corresponds to one pixel, 0 for black and 1 for white (typically it’s between 0 and 255 for grayscale images). The sliding window is called a kernel, filter, or feature detector. Here we use a 3×3 filter, multiply its values element-wise with the original matrix, then sum them up. To get the full convolution we do this for each element by sliding the filter over the whole matrix using a stride of 1. <cite>[ Understanding convolutional neural nets][3]</cite>

![alt text](http://deeplearning.stanford.edu/wiki/images/6/6c/Convolution_schematic.gif "Illustration of convolutional operation")

Source: http://deeplearning.stanford.edu/wiki/images

The parameters of the kernels or filters are typically trained by the network but you have to initialize the values of the parameters. Also typically using Deep Learning tools such as Tensor Flow, one has to specify how many kernels you want to train for the model. The more kernels the more parameter training. 

The output of the kernel multiplications are typically called feature maps. Below is an example of an image that has been blurred by using a filter/kernel:

![alt text](http://docs.gimp.org/en/images/filters/examples/generic-taj-convmatrix-blur.jpg "Blurring operation on an image")

Source: http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/

###CNNs

CNNs are basically just several layers of convolutions with nonlinear activation functions like ReLUs or tanhs applied to the result. These functions are used to capture non-linearity and especially the ReLUs lends themselves nicely to the derivation operation used in back-propagation in Neural Networks.  
In a typical feedforward neural network, we connect each input neuron to each output neuron in the next layer. This is called a fully connected layer. However, by conducting the convolution operation over the input we get so called sparse connectivity, meaning that not all inputs are connected to a neuron in the next layer. Each layer applies different filters, typically hundreds or thousands like the ones showed above, and combines their results. Typically a there are one or two fully connected layers following convolutions and max pooling operations.

![alt text](http://pubs.sciepub.com/ajme/2/7/9/image/fig2.png)

Source: http://pubs.sciepub.com/ajme/2/7/9/

These kernels are in terms learning to detect different features in an image such as edges etc. Once the network is more deeply connected it may also learn more high level features such as faces, buildings etc. 

![alt text](https://qph.ec.quoracdn.net/main-qimg-730164d3f54d38eb08808dcf4796c68b?convert_to_webp=true)

Source: http://docplayer.net/10387005-Image-classification-for-dogs-and-cats.html

A typically layer of a convolutional network consists of three stages. In the first stage, the layer performs several convolutions in parallel to produce a set of linear activations.  In the second stage each linear activation is run through a nonlinear activation function (RELUs etc.) This stage is called the detector stage. In the third stage pooling is used to modify the output layer further and is kind of dimensional reduction.

A pooling function replaces the output of the net at a certain location with a summary static of the nearby outputs.  For example Max pooling, which reports the maximum output in a matrix neighborhood.  There exist many of these functions such as average, l2 norm weighted average etc. 

![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Max_pooling.png/314px-Max_pooling.png "Max pooling")

The rationale behind this is that it helps to make the representation become approximately invariant to small translations of the input.  Invariance to translation means that if we translate the input by a small amount, the values of most of the pooled outputs do not change.

The three steps mentioned are usually repeated sequentially to capture more high-level features, until the last step which is predicting some task and essentially minimizing a loss function (softmax cross entropy) (e.g. if you have a dog, cat or a human in an image).

###CNNs in NLP

CNNs may also be used in NLP. If we have a sentence "I want an ice cream", our input matrix might be represented as an 5 (rows) x 100 (columns) matrix with one hot encoding for each word. Our filters will then typically be as wide as the input matrix but with variable length in terms of rows. The filters may cover 2-5 words. 

![alt text](http://d3kbpzbmcynnmx.cloudfront.net/wp-content/uploads/2015/11/Screen-Shot-2015-11-06-at-12.05.40-PM.png)

A big argument for using CNNs is that they are fast. Convolutions are a central part of computer graphics and implemented on a hardware level on GPUs. Compared to something like n-grams, CNNs are also efficient in terms of representation. With a large vocabulary, computing anything more than 3-grams can quickly become expensive. Even Google doesn’t provide anything beyond 5-grams. Convolutional Filters learn good representations automatically, without needing to represent the whole vocabulary. It’s completely reasonable to have filters of size larger than 5. I like to think that many of the learned filters in the first layer are capturing features quite similar (but not limited) to n-grams, but represent them in a more compact way.

My idea is to use CovNets as part inputs to recommendation systems in banking. For example, if a customer has a certain transactional pattern / email communication pattern (which in terms can be converted to text) it may have an explanation to what product the customer will take/or not take in the future. 

###CNN Terms

As this is supposed to be a high level intro to CNNs some important details have been omitted from this article. 
Here are couple:

* Patch  - Patch is usually the same as kernel/filter applied in the convolution process
* Stride - How many pixels you are shifting your filter when moving your kernel/filter
* Valid Padding - This has to do with where you start applying your filter. If you do not do anything in the edges (no padding) it is called valid padding. 
* Same Padding - Pad with 0s to make the input map and the output map roughly the same. 
* 1x1 Convolution – To come
* Inception Module – To come
* Channels - Channels are different “views” of your input data. For example, in image recognition you typically have RGB (red, green, blue) channels. You can apply convolutions across channels, either with different or equal weights. In NLP you could imagine having various channels as well: You could have a separate channels for different word embeddings (word2vec and GloVe for example), or you could have a channel for the same sentence represented in different languages, or phrased in different ways. <cite>[ Understanding convolutional neural networks for NLP][3]</cite>
* Dropouts – To come 

###CNN Future Projects

I will write some simple posts on practical cases using CNNs and TensorFlow. Here are some projects I plan to have a look at:

1. I will attempt to use review text to see what explanatory power language usage has to the ratings. I will try to use CNNs to predict the rating, to see whether the language features used in the past for a specific customer will have an explanatory effect on the current rating of a product (which I expect). http://sifaka.cs.uiuc.edu/~wang296/Data/LARA/Amazon/readme.txt. E.g. do customers that have a "rough" language have a bias towards giving low ratings etc. I will attempt to use a pre trained word2vec embeddings of review text as inputs in the network. (Word2Vec explanation) http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/2. 
2. Use CNNs with transactional text data to recommend the next bank product. The idea is that some transactional patterns may be explanatory to what product a bank customer may take as the next product. This predictive dimension will then be incorporated to the existing recommendation model. The goal is to see whether this model will improve the benchmark model. 

[1]:http://www.deeplearningbook.org
[2]:https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner's-Guide-To-Understanding-Convolutional-Neural-Networks-Part-2/
[3]:http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/

### References
1. Deep Learning, 2016, Ian Goodfellow, Yoshua Bengio, and Aaron Courville, Book in preparation for MIT Press
2. A Beginners Guide to Understanding Convolutional Neural Networks, https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner's-Guide-To-Understanding-Convolutional-Neural-Networks-Part-2/
3. Understanding convolutional neural networks for NLP, http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/
