---
layout: post
title: Modeling Rich Contexts for Sentiment Classification with LSTM
subtitle: Title of paper - Modeling Rich Contexts for Sentiment Classification with LSTM
category: NLP papers - Transfer_learning
tags: [neural_network, text_classification]
permalink: /2019/08/19/Modeling_Rich_Contexts_for_Sentiment_Classification_with_LSTM/
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

This is a brief summary of paper for me to study and organize it, [Modeling Rich Contexts for Sentiment Classification with LSTM, Huang et al., (2016)](https://arxiv.org/abs/1801.06146) I read and studied. 
{% include MathJax.html %}

They propose how to get representation with rich context in tweets which constitute a thread like conversation. 

![Huang et al., 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-08-19-Modeling_Rich_Contexts_for_Sentiment_Classification_with_LSTM/Hierachical_LSTM.JPG)

They used two types of LSTM, one is Word-level LSTM, the other is Tweet-level LSTM as above figure. 

The word-level encode a tweet into the fixed-size vector. 

and the Tweet-level use the vectors from word-level LSTM as input.

In other word, 

>> From Figure 2 we can see that in the word-level LSTM, the input is individual words.  
>> The hidden state of the last word is taken as the representation of the tweet.   
>> Each tweet in a thread will go through the word-level LSTM, and the t-th tweet in the thread will generate a tweet representation of zt which will be an input of the tweet-level LSTM.  

And the extend input of tweet level LSTM with context featues which represent as binary value.

The additional context feature is as follows:

- SameAuthor
- Converstaion
- SameHashtag
- SameEmoji


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Sentiment analysis on social media data such as tweets and weibo has become a very important and challenging task. Due to the intrinsic properties of such data, tweets are short, noisy, and of divergent topics, and sentiment classification on these data requires to modeling various contexts such as the retweet/reply history of a tweet, and the social context about authors and relationships. While few prior study has approached the issue of modeling contexts in tweet, this paper proposes to use a hierarchical LSTM to model rich contexts in tweet, particularly long-range context. Experimental results show that contexts can help us to perform sentiment classification remarkably better.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1605.01478">Modeling Rich Contexts for Sentiment Classification with LSTM</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Modeling Rich Contexts for Sentiment Classification with LSTM](https://arxiv.org/abs/1605.01478)
  
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)




























