---
layout: post
title: GhostWriter \: Using an LSTM for Automatic Rap Lyric Generation
subtitle: Title of paper - GhostWriter \: Using an LSTM for Automatic Rap Lyric Generation
category: NLP papers
tags: [nlp, lstm, nlg]
permalink: /2018/09/21/GhostWriter_Using_an_LSTM_for_Automatic_Rap_Lyric_Generation/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This paper's title is [GhostWriter: Using an LSTM for Automatic Rap Lyric Generation](http://www.aclweb.org/anthology/D15-1221) from EMNLP 2015

The model from this paper focus on generation of rap lyrics. the goal of Ghost Writer is to produce a system that can take a given artist's lyrics and generate similar yet unique lyrics.

They said the contributiono of their paper like this:

- They said "we present the ghostwriting problem of producing similar yet differenct lyrics"

- They said "we present computational, quantitative evaluation methods for these twe aspects"

- They said "we evaluate the performance of a Long Short-Term Memory(LSTM) vs n-gram model for this problem"

their goal to build model is the model doesn't require templates/constrains to generate lyrics and the model is able to produce full verses, as opposed to single lies.

The model can alos imitate the lyrics style of a target artist by understanding the artist's vocabulary and rhythmic style.

Fron now on, I summarized the argument against their model. 

Let's See how to use LSTM for generation of lyrics. 

I think they used **word embedding** to a LSTM, they used on each word learn a LSTM's new representation of word embedding with sequence information. 

They hope LSTM can captures the rhythmic style of an artist by learning rhyme and meter patters.

They said the goal of their model is to not just generate lyrics, but generate the structure for the lyrics as well. 

For their goal, They used some tokens like this :

> "<endLine>", "<endVerse>"

They said they expect the system will generate its own line break(<endLine>) and define when the generated verse ends(<endVerse>).

They expected one thing more from "<endLine>", It is the system has a better chancd of understading rhyme schemes used by an artist.


### Their dataset

They collected songs from [The Original Hip-Hap (Rap) Lyrics Achive - OHHLA.com - Hip-Hop Since 1992](http://www.ohhla.com)

They also used a paticular artist, Fabolous. because his lyrics produced highest accuracy in the artist recognition experiments in (Hirjee and Brown, 2010a).

For performance, they used a comparable model which is markov model for lyrics generation based on N-gram method.

In the case of n-gram model, they used back-off to a smaller n-gram against the probability that the context has been never encountered in training data.

Their model's initialization used "<startVerse>" token.

When producing lyrics with either the LSTM or baseline model. they said "we initialize  with the "<strtVerse>" token.

They used python implementation of an LSTM  from [Jonathan Raiman](https://github.com/JonathanRaiman/theano_lstm).

<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
word embedding, LSTM, some tokens(<endLine>, <endVerse>, <startVerse), morkov model(n-gram base), language model,
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
This ppaer demonstrate the effectiveness to generate unconstrained rap lyrics using a Long Short-Term Memory Language Model. In this paper, the goal generates lyrics in style to that of a given rapper(Fabolous) but the generated lyrics are not identical to exiting lyrics. it is call ghostwriting task in this paper. It is also different than previous model using explicit templates. Their model defines its own rhyme scheme, line length, and verse length.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://aclanthology.coli.uni-saarland.de/papers/D15-1221/d15-1221">The paper: GhostWriter: Using an LSTM for Automatic Rap Lyric Generation</a>
</div>

# Reference 

- Paper 
  - [GhostWriter: Using an LSTM for Automatic Rap Lyric Generation](https://aclanthology.coli.uni-saarland.de/papers/D15-1221/d15-1221)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html) 
