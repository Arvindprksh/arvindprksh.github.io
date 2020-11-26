---
layout: post
title: Targeted Syntactic Evaluation of Language Models
subtitle: Title of paper - Targeted Syntactic Evaluation of Language Models
category: NLP papers - Language Model
tags: [language model, syntactic property]
permalink: /2020/11/26/What_do_you_learn_from_context_Probing_for_sentence_structure_in_contextualized_word_representations/
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

This is a brief summary of paper for me to study and organize it, [Targeted Syntactic Evaluation of Language Models (Marvin and Linzen., EMNLP 2018)](https://www.aclweb.org/anthology/D18-1151/)
   that I read and studied. 
{% include MathJax.html %}

They investigated the ability related to capturing in syntax with LSTM-based langauge model. 

They point out that The quality of the syntactic predictions made by the LM is arguably particularly difficult to measure using perplexity, which is evaluation method for Language model, since most sentences are grammatically simple and most words can be predicted from their local context, perplexity rewards language models primarily for collocational and semantic predictions.

So they evaluation of grammaticality on a number of minimally different pairs of English sentence.

For experiment, to discrimnate which one is grammatical or ungrammartical sentence, they made dataset as follows (i.e. \* mark is syntactically wrong sentence):

For Subject-verb agreement, 

(1) Simple agreement:
    a. The author **laughs**.
    b. \*The author **laugh**.

(2) Agreement in a sentential complement:
    a. The bankers knew the officer **smiles**.
    b. *The bankers knew the officer **smile**.

(3) Agreement across a prepositional phrase:
    a. The farmer near the parents **smiles**.
    b. \*The farmer near the parents **smile**.

(3) Agreement across a subject relative clause:
    a. The officers that love the skater **smile**.
    b. \*The officers that love the skater **smiles**.

(4) Short VP coordination:
    a. The senator smiles and **laughs**.
    b. \*The senator smiles and **laugh**.
    
(5) Long VP coordination:
    The manager writes in a journal every day and likes/*like to watch television shows.

(6) Agreement across an object relative clause(including **no that**):
    a. The farmer that the parents love **swims**.
    b. \*The farmer that the parents love **swim**.

(7) Agreement in an object relative clause(including **no that**):
    a. The farmer that the parents **love** swims.
    b. \*The farmer that the parents **loves** swims.

For Reflexive anaphora,

(1) Simple reflexive:
   a. The senators embarrassed themselves.
   b. \*The senators embarrassed herself.

(2) Reflexive in a sentential complement:
   a. The bankers thought the pilot embarrassed himself.
   b. \*The bankers thought the pilot embarrassed themselves

(3) Reflexive across an object relative clause:
   a. The manager that the architects like doubted himself.
   b. \*The manager that the architects like doubted themselves.


For  Negative polarity items,

(1) Simple NPI:
   a. **No** students have ever lived here.
   b. \***Most** students have ever lived here.


(2) NPI across a relative clause:
   a. **No** authors that **the** security guards like have ever been famous.
   b. \***The** authors that **no** security guards like have ever been famous.

To show how our challenge set can be used to evaluate the syntactic performance of LMs with cases above, they trained three language models with increasing levels of syntactic sophistication. All of the language models were trained on a 90 million word subset of Wikipedia.

The type of language models for experiment is  n-gram and LSTM (i.e. single-task and multi-task language model).

Their n-gram LM and LSTM language model do not require annotated data. The third model is also an LSTM language model (i.e. multi-task language model), but it requires syntactically annotated data (CCG supertags).


they have described a template-based data set for targeted syntactic evaluation of language models.

The data set consists of pairs of sentences that are matched except for their grammaticality.

They consider a language model to capture the relevant aspects of the grammar of the language if it assigns a higher probability to the grammatical sentence than to the ungrammatical one.

An RNN language model performed very well on local subject-verb agreement dependencies, significantly outperforming an n-gram baseline.

Even on simple cases, however, the RNN’s accuracy was sensitive to the particular lexical items that occurred in the sentence, this would not be expected if its syntactic representations were fully abstract. 

The RNN’s performance degraded markedly on non-local dependencies, approaching chance levels on agreement across an object relative clause. 

Multi-task training with a syntactic objective (CCG supertagging) mitigated this drop in performance for some but not all of the dependencies they tested. 

They conjectured that the benefits of the inductive bias conferred by multi-task learning will be amplified when the amount of training data is limited.

For detailed experiment analysis, you can found in [Targeted Syntactic Evaluation of Language Models (Marvin and Linzen., EMNLP 2018)](https://www.aclweb.org/anthology/D18-1151/)
  
<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They present a dataset for evaluating the grammaticality of the predictions of a language model. They automatically construct a large number of minimally different pairs of English sentences, each consisting of a grammatical and an ungrammatical sentence. The sentence pairs represent different variations of structure-sensitive phenomena: subject-verb agreement, reflexive anaphora and negative polarity items. They expect a language model to assign a higher probability to the grammatical sentence than the ungrammatical one. In an experiment using this data set, an LSTM language model performed poorly on many of the constructions. Multi-task training with a syntactic objective (CCG supertagging) improved the LSTM’s accuracy, but a large gap remained between its performance and the accuracy of human participants recruited online. This suggests that there is considerable room for improvement over LSTMs in capturing syntax in a language model
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D18-1151">The paper: Targeted Syntactic Evaluation of Language Models (Marvin and Linzen., EMNLP 2018)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Targeted Syntactic Evaluation of Language Models (Marvin and Linzen., arXiv 2018)](https://arxiv.org/abs/1808.09031)
  - [EMNLP Version: Targeted Syntactic Evaluation of Language Models (Marvin and Linzen., EMNLP 2018)](https://www.aclweb.org/anthology/D18-1151/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


