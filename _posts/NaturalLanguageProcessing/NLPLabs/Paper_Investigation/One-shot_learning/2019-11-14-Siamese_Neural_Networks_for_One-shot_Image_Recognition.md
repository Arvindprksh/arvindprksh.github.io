---
layout: post
title: Siamese Neural Networks for One-shot Image Recognition
subtitle: Title of paper - Siamese Neural Networks for One-shot Image Recognition
category: papers - One(Few or zero)-shot learning
tags: [neural network, image classification]
permalink: /2019/11/14/Siamese_Neural_Networks_for_One-shot_Image_Recognition/
css : /css/ForYouTubeByHyun.css
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
  
---

This is a brief summary of paper for me to study and organize it, [Siamese Neural Networks for One-shot Image Recognition (Koch et al. 2015)](http://www.cs.toronto.edu/~rsalakhu/papers/oneshot1.pdf) I read and studied. 
{% include MathJax.html %}

They said whta one-shot learning is:

>> we may only observe a single example of each possible class before making a prediction about a test instance. This is called one-shot learnig. It is different from zero-shot learning, in which the model cannot look at any example from the target classes.

Their approach to one-shot learning is to use siamese convolutional neural network's features without any retraing.

They hypothesize that networks which do well at verification should generalize to one-shot classification. i.e. the verfication model learns to identify input pairs according to the probability that they belong to the same class or different class. They used the verification model to evaluate new images, exactly one per novel class, in a pairwise manner against the test images.

ahead of entering siamese convolutional neural network, Let's see the siamese network: 

![Koch et al. 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/One-shot_learning/2019-11-14-Siamese_Neural_Networks_for_One-shot_Image_Recognition/siamese_network.PNG)

The Siamese neural network consists of twin networks which accept distinct inputs but are joined by an energy function(e.g. a loss function) at the top.

The function computes some metric between the highest-level feature representation on each side above image.

Their model's architecture : 

Below show one example of twin networks. 

![Koch et al. 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/One-shot_learning/2019-11-14-Siamese_Neural_Networks_for_One-shot_Image_Recognition/siamese_convolutional_1.PNG
)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
The process of learning good features for machine learning applications can be very computationally expensive and may prove difficult in cases where little data is available. A prototypical example of this is the one-shot learning setting, in which They want to correctly make predictions given only a single example of each new class. In their paper, they explore a method for learning siamese neural networks which employ a unique structure to naturally rank similarity between inputs. Once a network has been tuned, they can then capitalize on powerful discriminative features to generalize the predictive power of the network not just to new data, but to entirely new classes from unknown distributions Using a convolutional architecture.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="http://www.cs.toronto.edu/~rsalakhu/papers/oneshot1.pdf">The paper: Siamese Neural Networks for One-shot Image Recognition (Koch et al. 2015)</a>
</div>

# Reference 

- Paper 
  - [Siamese Neural Networks for One-shot Image Recognition (Koch et al. 2015)](http://www.cs.toronto.edu/~rsalakhu/papers/oneshot1.pdf)
  
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [Siamese Neural Networks for One-Shot Image Recognition by Koch](http://www.cs.toronto.edu/~gkoch/files/msc-thesis.pdf)
  - [Meta-Learning: Learning to Learn Fast on Lil'Log](https://lilianweng.github.io/lil-log/2018/11/30/meta-learning.html)
  - [Learning to Learn on BAIR](https://bair.berkeley.edu/blog/2017/07/18/learning-to-learn/)
  - [Omniglot dataset github](https://github.com/brendenlake/omniglot/tree/057f034baf2ecb8530bc5710e5a23584d2a519cc)






























