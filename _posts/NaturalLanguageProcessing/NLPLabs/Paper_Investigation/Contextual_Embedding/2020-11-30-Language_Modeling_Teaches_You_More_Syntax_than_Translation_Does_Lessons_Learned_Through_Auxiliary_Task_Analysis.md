---
layout: post
title: Language Modeling Teaches You More Syntax than Translation Does- Lessons Learned Through Auxiliary Task Analysis 
subtitle: Title of paper - Language Modeling Teaches You More Syntax than Translation Does- Lessons Learned Through Auxiliary Task Analysis 
category: NLP papers - Contextual Embedding
tags: [contextual Embedding]
permalink: /2020/11/30/Language_Modeling_Teaches_You_More_Syntax_than_Translation_Does_Lessons_Learned_Through_Auxiliary_Task_Analysis/
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

This is a brief summary of paper for me to study and organize it, [Language Modeling Teaches You More Syntax than Translation Does: Lessons Learned Through Auxiliary Task Analysis (Zhang and Bowman, under review in ICLR 2019)](https://openreview.net/forum?id=ryeNPi0qKX) that I read and studied. 
{% include MathJax.html %}

They investigated how well LSTM-based models with various training method induces syntactic information into their hidden representation, following that recently, researchers have begun to investigate the properties of learned representations by training auxiliary
classifiers that use the hidden states of frozen, pretrained models to perform other tasks.. 

In order to analyze the property of how well they encode syntactic information, they implemented tasks such as POS tagging, CCG supertagging, and word idetity prediction.

Let's see What is the POS tagging and CCG supertaging task, they are:

![Zhang and Bowman, ICLR 2019](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2020-11-30-Language_Modeling_Teaches_You_More_Syntax_than_Translation_Does_Lessons_Learned_Through_Auxiliary_Task_Analysis/POS_N_CCG.PNG)

for word identity prediction task, it is : 

>> for the sentence “I love NLP” and a time step shift of -2, we would train the classifier to take the hidden state for “NLP” and predict the word “I”.

for LSTM-based models to experiment how well they encode syntactic information into their hidden representation, they use bidirectional Language model, neural machiane translation, skip-thought, autoencoding, and untrained LSTM. 

Their experiments focus on questions below:

1. How does the training task affect how well models learn syntactic properties? Which tasks are better at inducing these properties?
2. How does the amount of data the model is trained on affect these results? When does training on more data help?

They investigate these questions by holding the data source and model architecture constant, while varying both the training task and the amount of training data. 

Specifically, they examine models trained on English-German (En-De) translation, language modeling, skip-thought ([Kiros et al.,2015](https://papers.nips.cc/paper/2015/file/f442d33fa06832082290ad8544a8da27-Paper.pdf)), and autoencoding, and also compare to an untrained LSTM model as a baseline.

by controlling for the data domain by exclusively training on datasets from the 2016 Conference on Machine Translation, they make fair comparisons between several data-rich training tasks in their ability to induce syntactic information. 

They found that bidirectional language models (BiLMs) do better than translation and skip-thought encoders at extracting useful features for POS tagging and CCG supertagging. 

Moreover, this improvement holds even when the BiLMs are trained on substantially less data than competing models. 

Especially, for word identity prediction, they found that all trained LSTMs underperform untrained ones on word identity prediction. 

This finding confirms that trained encoders genuinely capture substantial syntactic features, beyond mere word identity, that the auxiliary classifiers can use. 

Their results suggest that for transfer learning, BiLMs like ELMo ([Peters et al., 2018](https://www.aclweb.org/anthology/N18-1202/)) capture more useful features than translation encoders—and that this holds even on genres for which data is not abundant.

They also find that randomly initialized encoders extract usable features for POS and CCG tagging at least when the auxiliary POS and CCG classifiers are themselves trained on reasonably large amounts of data. 

The performance of untrained models drops sharply relative to trained ones when using smaller amounts of the classifier data. 

They investigate further and find that untrained models outperform trained ones on the task of neighboring word identity prediction, which confirms that trained encoders do not perform well on tagging tasks because the classifiers are simply memorizing word identity information. 

They also find that both trained and untrained LSTMs store more local neighboring word identity information in lower layers and more distant word identity information in upper layers, which suggests that depth in LSTMs allow them to capture larger context information.

For detailed experiment analysis, you can found in [Language Modeling Teaches You More Syntax than Translation Does: Lessons Learned Through Auxiliary Task Analysis (Zhang and Bowman, under review in ICLR 2019)](https://openreview.net/forum?id=ryeNPi0qKX)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Recent work using auxiliary prediction task classifiers to investigate the properties of LSTM representations has begun to shed light on why pretrained representations, like ELMo ([Peters et al., 2018](https://www.aclweb.org/anthology/N18-1202/)) and CoVe ([McCann et al., 2017](https://papers.nips.cc/paper/2017/hash/20c86a628232a67e7bd46f76fba7ce12-Abstract.html)), are so beneficial for neural language understanding models. They still, though, do not yet have a clear understanding of how the choice of pretraining objective affects the type of linguistic information that models learn. With this in mind, they compare four objectives—language modeling, translation, skip-thought, and autoencoding—on their ability to induce syntactic and part-of-speech information. They make a fair comparison between the tasks by holding constant the quantity and genre of the training data, as well as the LSTM architecture. They find that representations from language models consistently perform best on our syntactic auxiliary prediction tasks, even when trained on relatively small amounts of data. These results suggest that language modeling may be the best data-rich pretraining task for transfer learning applications requiring syntactic information. They also find that the representations from randomly-initialized, frozen LSTMs perform strikingly well on our syntactic auxiliary tasks, but this effect disappears when the amount of training data for the auxiliary tasks is reduced.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://openreview.net/forum?id=ryeNPi0qKX">The paper: Language Modeling Teaches You More Syntax than Translation Does: Lessons Learned Through Auxiliary Task Analysis (Zhang and Bowman, under review in ICLR 2019)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Language Modeling Teaches You More Syntax than Translation Does: Lessons Learned Through Auxiliary Task Analysis (Zhang and Bowman, arXiv 2019)](https://arxiv.org/abs/1410.8206)
  - [ICLR Version: Language Modeling Teaches You More Syntax than Translation Does (Zhang and Bowman, under review in ICLR 2019)](https://openreview.net/forum?id=ryeNPi0qKX)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


