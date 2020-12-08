---
layout: post
title: Deep Semantic Role Labeling- What Works and What’s Next
subtitle: Title of paper - Deep Semantic Role Labeling- What Works and What’s Next
category: NLP papers - SRL
tags: [SRL]
permalink: /2020/12/08/Deep_Semantic_Role_Labeling_What_Works_and_Whats_Next/
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

This is a brief summary of paper for me to study and organize it, [Deep Semantic Role Labeling: What Works and What’s Next (He et al., ACL 2017)](https://www.aclweb.org/anthology/P17-1044/) that I read and studied. 
{% include MathJax.html %}

Semantic role labeling (SRL) systems aim to recover the predicate-argument structure of a sentence, to determine essentially “who did what to whom”, “when”, and “where.”

Recently breakthroughs involving end-to-end deep models for SRL without syntactic input seem to overturn the long-held belief that syntactic parsing is a prerequisite for this task.

So treating SRL as a BIO tagging problem, they propose end-to-end deep neural model with bidirectional LSTMs as follow: 

![He et al., ACL 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-12-08-Deep_Semantic_Role_Labeling_What_Works_and_Whats_Next/deep_SRL_model.PNG)

As shown in the figure above, the bidirectional LSTMs they used in their experiment is alternative structure. 

Formally, their task is to predict a sequence \\(y\\) given a sentence-predicate pair \\((w, v)\\) as input. Each \\(y_i \in y\\) belongs to a discrete set of BIO tags \\(T\\).

Words outside argument spans have the tag \\(O\\), and words at the beginning and inside of argument spans with role \\(r\\) have the tags \\(B_r\\) and \\(I_r\\) respectively. 

Let \\(n = \|w\| = \|y\|\\) be the length of the sequence.

They also used a variety of deep learning techiniques:

- highway connection 
- RNN-Dropout
- A\* decoding algorithms 
- some constraints: BIO constraints, SRL constraints, Syntactic constraints

For detailed experiment analysis and in-depth model architectur and constraints, you can found in [Deep Semantic Role Labeling: What Works and What’s Next (He et al., ACL 2017)](https://www.aclweb.org/anthology/P17-1044/)
  

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They introduce a new deep learning model for semantic role labeling (SRL) that significantly improves the state of the art, along with detailed analyses to reveal its strengths and limitations. They use a deep highway BiLSTM architecture with constrained decoding, while observing a number of recent best practices for initialization and regularization. Extensive empirical analysis of these gains show that (1) deep models excel at recovering long-distance dependencies but can still make surprisingly obvious errors, and (2) that there is still room for syntactic parsers to improve these results.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P17-1044/">The paper: Deep Semantic Role Labeling: What Works and What’s Next (He et al., ACL 2017)</a>
</div>

# Reference 

- Paper 
  - [ACL Version: Deep Semantic Role Labeling: What Works and What’s Next (He et al., ACL 2017)](https://www.aclweb.org/anthology/P17-1044/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


