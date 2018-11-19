---
layout: post
title: How to do padding in Tensorflow 
subtitle: There are two types of padding, SAME and VALID
category: Tensorflow
tags: [tensorflow]
permalink: /2018/07/23/Tensorflow's_Neural_Network_Convolution/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/05.Convolution/01-Tensorflow%27s%20Neural%20Network%20Convolution.ipynb-->

# Tensorlfow's Neural Network Convolution

The convolution ops convolves a 2-D filter over a batch of images, applying the filter to each window of each image of the appropriate size. There are different verions of filter between generic vs. specific filters.

  - **conv2d:** Arbirtrary filters that can mix channels(R, G, B) together.
  
  - **depthwise_conv2d:** Filters that operate on each channel independently.
  
  - **separable_conv2d:** A depthwise spatial filter followed by a pointwise filter.
  
except for thigs above, Tensorflow is providing several version of convolution filter, BUT, in here, I would explain padding scheme with conv2d like this:


![Kim, Y. (2014). Convolutional Neural Networks for Sentence Classification](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_Machine_Learning/master/Tutorial/Tensorflow/05.Convolution/Images/01-Tensorflow-s_Neural_Network_Convolution/Convolutional_Neural_Networks_for_Sentence_Classification.png)

i.e. As you can see above, I am going to convolve a window of a sentence with conv2d filter. 


The filter is applied to image patches of the same size as the filter and strided acoording to strides argument. 

the argument is strides=[1, 1, 1, 1], it means every offset to move the filter, each postion of strides argument from left means batch, height, width, channel(e.g. NHWC format).

Ignoring channels for the moments, assume that the 4-D input has shape of [batch, input_height, input_width, input_channels] and the 4-D filter has shape [filter_height, filter_width, input_channel, output_channel]. The spatial of the convolution ops depend on the padding scheme chosen: "SAME" or "VALID".

From now on, if I say padding, it means zero padding. i.e. I am always padding zero value like this.

![http://cs231n.github.io/convolutional-networks/](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_Machine_Learning/master/Tutorial/Tensorflow/05.Convolution/Images/01-Tensorflow-s_Neural_Network_Convolution/cs231_conv.png)



## SAME Scheme 

"SAME" Scheme mean height and width size is the same between input and output. i.e. "SAME" scheme always pad zero value to evaluate edge part of image. 

Tensorflow's "SAME" padding scheme use the smallest possible padding to achive the desired output size.

If you want to know about SAME scheme more, visit [Notes on SAME Convolution padding](https://www.tensorflow.org/versions/r1.8/api_guides/python/nn#Notes_on_SAME_Convolution_Padding)

{% highlight python linenos %}
import numpy as np

input_height = 4 # Image Height
input_width = 300 # Image Width

filter_height = 2 # filter Height
filter_width = 300 # filter Width


# batch, height, width, channel
strides = [1, 1, 1, 1]

# Same Scheme : padding like things below

float_height = float(input_height) / float(strides[1])
float_width = float(input_width) / float(strides[2])
output_height = np.ceil(float_height)
output_width = np.ceil(float_width)

print("====== Under SAME Scheme ======")
print("output_height: {}".format(output_height))
print("output_width: {}".format(output_width))
print()
{% endhighlight %}


{% highlight linenos %}
====== Under SAME Scheme ======
output_height: 4.0
output_width: 300.0
{% endhighlight %}

As you can see above, input height and input width is the same from output height and output width.
finally, the padding on top, bottom, left and right are :

{% highlight python linenos %}
# SAME Scheme
if (input_height % strides[1] == 0):
    pad_along_height = max(filter_height - strides[1], 0)
else:
    pad_along_height = max(filter_height - (input_height % strides[1]), 0)
if (input_width % strides[2] == 0):
    pad_along_width = max(filter_width - strides[2], 0)
else:
    pad_along_width = max(filter_width - (input_width % strides[2]), 0)

    
print("pad along height and width...")
print("pad along height: {}".format(pad_along_height))
print("pad along width: {}".format(pad_along_width))
pad_top = pad_along_height // 2 # divied by 2
pad_bottom = pad_along_height - pad_top
pad_left = pad_along_width // 2
pad_right = pad_along_width - pad_left    

print("Padding size on top, bottom, left and right")
print("top: {}".format(pad_top))
print("bottom: {}".format(pad_bottom))
print("left: {}".format(pad_left))
print("right: {}".format(pad_right))
{% endhighlight %}


{% highlight linenos %}
pad along height and width...
pad along height: 1
pad along width: 299
Padding size on top, bottom, left and right
top: 0
bottom: 1
left: 149
right: 150

{% endhighlight %}

in the above case, there are the division by 2 to separate padding in height to top and bottom, also padding in weight to left and right. in this case, the bottom and right sides always get the one additional padded pixel.

This method is different from the others libraries such as cuDNN and Caffe, which explicitly specify the number of padded pixels and always pad the same number of pixels on both sides. 

## VALID Scheme on padding 

"VALID" scheme don't use padding. 

So if you use "VALID" scheme, output size shrinks.

The following is a example.

{% highlight python linenos %}
input_height = 5 # Image Height
input_width = 5 # Image Width

filter_height = 3 # filter Height
filter_width = 3 # filter Width

# Valid Scheme : no padding is used.

float_height = float(input_height - filter_height + 1) / float(strides[1])
float_width = float(input_width - filter_width + 1) / float(strides[2])
output_height = np.ceil(float_height)
output_width = np.ceil(float_width)

print("====== Under VALID Scheme ======")
print("output_height: {}".format(output_height))
print("output_width: {}".format(output_width))
print("VALID Schem is no padding")
{% endhighlight %}

{% highlight linenos %}
====== Under VALID Scheme ======
output_height: 3.0
output_width: 3.0
VALID Schem is no padding
{% endhighlight %}

The result of convolution can be computed as follows. i.e. conv computation is linear function like : F(x)=xW+b

If the following is using "VALID" Scheme, as you could see, its output height size and width size is the same from the evaluation of code above.

![http://deeplearning.stanford.edu/wiki/images/6/6c/Convolution_schematic.gif](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_Machine_Learning/master/Tutorial/Tensorflow/05.Convolution/Images/01-Tensorflow-s_Neural_Network_Convolution/Convolution_schematic.gif)

Given the output size and the padding, the output can be computed as:

{% highlight python linenos %}
from IPython.display import Math
Math(r"output[b, i, j, :] = sum_{d_i, d_j} input[b, strides[1] * i + d_i - pad_{top},\
                           strides[2] * j + d_j - pad_{left}, ...] *filter[d_i, d_j,\ ...]")
{% endhighlight %}
output[b,i,j,:]=sumdi,djinput[b,strides[1]∗i+di−padtop,strides[2]∗j+dj−padleft,...]∗filter[di,dj, ...]
{% highlight linenos %}

Where any value outside the orginal input image resion are considered zero (i.e. padding value around the border of the image is always zero).

# Reference 

 - [Tensorlfow's Neural Network Convolution ver 1.8](https://www.tensorflow.org/versions/r1.8/api_guides/python/nn#Convolution)
 
 - [Tensorflow's the smallest padding on SAME Scheme](https://www.tensorflow.org/versions/r1.8/api_guides/python/nn#Notes_on_SAME_Convolution_Padding)
{% endhighlight %}
