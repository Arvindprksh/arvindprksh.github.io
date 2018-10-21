---
layout: post
title: A Taxonomy for Neural Memory Networks
subtitle: Title of paper - A Taxonomy for Neural Memory Networks
category: neural network papers
tags: [neural_network, memory_network]
permalink: /2018/10/22/A_Taxonomy_for_Neural_Memory_Networks/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This article is just brief summary of [A Taxonomy for Neural Memory Networks](https://arxiv.org/pdf/1805.00327v1.pdf) and posting for me to study what the memory network is. 

They suggest A taxonomy for Neural Memory Network with RNN, LSTM, Neural Stack, and Neural RAM.

Memory network has two focuses on the memory which are memory  depth  (how  much  the  past is remembered) and memory resolution (how specifically the system remembers a past event).

due to this focuses, Memory structure become complex to remember the depth and the resolution better.

Let's see the taxonmoy they said for memory network. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Neural_Network/2018-10-22-A_Taxonomy_for_Neural_Memory_Networks/A_Taxonomy_for_Neural_Memory_Network_Taxonomy.png)

From now on, I will deal with the the components of taxonomy for memory network. 

## Vanillna RNN

As you can see below, The RNN network is composed of three layers: input, recurrent hidden, and output laye. Besides all the feed forward connections, their is a feedback connection from hidden layer to itself.

In this paper, the basic RNN structure is described as follows:

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Neural_Network/2018-10-22-A_Taxonomy_for_Neural_Memory_Networks/A_Taxonomy_for_Neural_Memory_Network_RNN.png)


## LSTM 

Long short term memory was proposed to provide more flexibility to RNNs by employing an external memory called **cell state** to deal with the vanishing gradient problem.

Three logic gates are also introduced to adjust this external memory(cell state) and internal memory(hidden state).

But LSTM has a problem which is difficult to accomplish some simple memorization tasks such as copying and reversing a sequence. 

i.e. LSTM and its variants is that previous memories are erased after they are updated.

In this paper, the basic LSTM structure is described as follows:

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Neural_Network/2018-10-22-A_Taxonomy_for_Neural_Memory_Networks/A_Taxonomy_for_Neural_Memory_Network_LSTM.png)


Another case : 

LSTM has a problem that the previous memory is erased after it is updated. So there is another architecture to resolve the problem as follows.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Neural_Network/2018-10-22-A_Taxonomy_for_Neural_Memory_Networks/A_Taxonomy_for_Neural_Memory_Network_with_LTSM_parallel_memory_slot.png)

## Neural stack 

Neural stack is an example which uses a stack as its external memory bank and gets access to stack the topmost content through **push**, **pop**, and **no-op** operations.

In this paper, the basic Neural stack structure is described as follows:

![](img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Neural_Network/2018-10-22-A_Taxonomy_for_Neural_Memory_Networks/A_Taxonomy_for_Neural_Memory_Network_Neural_stack.png)

To sum up, one stack property is that only the topmost content of the stack can be read or written. Writing to the stack is implemented by three operations:

 - push : adding an element to the top of the stack.
 
 - pop : removing the topmost of the stack.
 
 - no-operation : Keeping the stack unchanged. 

If you want to know stak operation on neural stack, read [this paper,Inferring Algorithmic Patterns with Stack-Augmented Recurrent Nets](https://arxiv.org/abs/1503.01007).

They followed Inferring Algorithmic Patterns with Stack-Augmented Recurrent Nets on operation of Neural stack they said:

## Neural RAM

Neural stack' content could be access on the topmost content, But There is more powerful momory network structure that is all contents in the memory bank can be accessed.

i.e. since Neural RAM's accessible content is not restricted to the top of the memory as neural stack, Neural RAM has more flexibility to handle its memory bank.


In this paper, the basic Neural RAM structure is described as follows:

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Neural_Network/2018-10-22-A_Taxonomy_for_Neural_Memory_Networks/A_Taxonomy_for_Neural_Memory_Network_Neural_RAM.png)

As you can see above, The neural RAM  can be seen as an improvement of the neural stack in the sense that all the contents in the memory bank can be read from and written to.

But There is a challeng of neural RAM is that all the memory addresses are discrete in nature. 

I mean the neural RAM can be learned by backpropagation. the read and write addresses have to be continous. 

for the solution of this difficulty :

 - In the Neural RAM field, reading and writing to all the positions with different strengths is used.
 
Those strengths can also be explained as the probabilities each position would be read from and written to.

One thing to note is that the read and write position do not need to be the same ones.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Their Taxonomy includes all the popular memory networks; vanilla recurrent neural network(RNN), long-short term memory(LSTM), neural stack, and neural RAM. In their paper, the difference and commonality between these networks are analyzed. they saed the difference is divided on depending on the specific task for using memory network.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1805.00327v1">The paper: A Taxonomy for Neural Memory Networks</a>
</div>

# Reference 

- Paper 
  - [A Taxonomy for Neural Memory Networks](https://arxiv.org/abs/1805.00327v1)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
 


































