---
layout: post
title: The Curious Case of Neural Text Degeneration
subtitle: Title of paper - The Curious Case of Neural Text Degeneration
category: NLP papers - Translation
tags: [neural network, translation]
permalink: /2020/06/04/The_Curious_Case_of_Neural_Text_Degeneration/
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

This is a brief summary of paper for me to note it, [The Curious Case of Neural Text Degeneration. Holtzman et al. ICLR 2020](https://openreview.net/forum?id=rygGQyrFvH)

{% include MathJax.html %}

Despite considerable advances in neural language modeling with the maximization-based method which lead to high quality models for a range of language understanding tasks. 

They point out the problems of the current text generation that based on the maximization-based decoding method. 

The text generation with the maximization-based decoding method such as beam-search is bland, incoherent, and get stuck in repetitive loops.

So they propose the new decoding strategy which the call **Nucleus Sampling**. 

Let's see futher basic concept about text generation.

A number of recent works have alluded to disadvantage of maximization-based generation, which tends to generate output with high grammaticality but low diversity.

Generative Adversarial Networks have been a prominent research direction, but it is worse than language model in jointly considering generation's quality and diversity.

Meanwhile, Anoter approach give a rise to beam search tweaking scoring function for task-specific diversity.

Also they split the field of generation into two fileds which are Open-ended and directed generation. 

Many text generation tasks are defined through (input, output) pairs, such that the output is a constrained transformation of the input. 

Example applications include machine translation, data-to-text generation, and summarization that they refered to as **directed generation**

Another approach, open-ended generation, includes conditional stroy generation and contextual text continuation. They also think of goal-oriented dialog as between open-ended generation and directed generation.

From now on, Let's see several decoding strategies they explained. 

1. Maximization-based decoding.

>>The most commonly used decoding objective, in particular for directed generation, is maximization-based decoding.  
>>Assuming that the model assigns higher probability to higher quality text, 
>>these decoding strategies search for the continuation with the highest likelihood.   
>>Since finding the optimum argmax sequence from recurrent neural language models or Transformers is not tractable,  
>>common practice is to use beam search. 

2. Nucleus sampling

>> a new stochastic decoding method: Nucleus Sampling. The key idea is to use the shape of the probability distribution to determine the set of tokens to be sampled from. 

3. Top-k sampling

>>Nucleus Sampling and top-k both sample from truncated Neural LM distributions, differing only in the strategy of where to truncate.  
>>Choosing where to truncate can be interpreted as determining the generative model’s trustworthy prediction zone.

4.  Sampling with temperature

>>Another common approach to sampling-based generation is to shape a probability distribution through temperature.

------- 
When they generate target sentence, they use a basic form of beam-search to find a translation that maximizes the conditional probability given by a specific models.

it is better than [Greed search](https://youtu.be/Er2ucMxjdHE).  

If you want to know what beam-search is, see the following (e.g. Youtube lecture)

<div id="tutorial-section">

  <div id="tutorial-title">Youtube of Deeplearning Ai</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">Greedy Search</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept">Beam search</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept2">Refinements to beam search</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept3">Error Analysis of Beam Search</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/Er2ucMxjdHE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div id="refrigerator_concept" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/RLWuzLLSIgw?list=PLCSzVeDv57Z1y0uWZXYX2kq5UUpqA0Mk2" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
     <div id="refrigerator_concept2" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/gb__z7LlN_4?list=PLCSzVeDv57Z1y0uWZXYX2kq5UUpqA0Mk2" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> 
     </div>
    <div id="refrigerator_concept3" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/ZGUZwk7xIwk?list=PLCSzVeDv57Z1y0uWZXYX2kq5UUpqA0Mk2" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
     </div>
  </div>
 
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Despite considerable advances in neural language modeling, it remains an open question what the best decoding strategy is for text generation from a language model (e.g. to generate a story). The counter-intuitive empirical observation is that even though the use of likelihood as training objective leads to high quality models for a broad range of language understanding tasks, maximization-based decoding methods such as beam search lead to degeneration — output text that is bland, incoherent, or gets stuck in repetitive loops. To address this they propose Nucleus Sampling, a simple but effective method to draw considerably higher quality text out of neural language models than previous decoding strategies. Their approach avoids text degeneration by truncating the unreliable tail of the probability distribution, sampling from the dynamic nucleus of tokens containing the vast majority of the probability mass. To properly examine current maximization-based and stochastic decoding methods, they compare generations from each of these methods to the distribution of human text along several axes such as likelihood, diversity, and repetition. Their results show that (1) maximization is an inappropriate decoding objective for openended text generation, (2) the probability distributions of the best current language models have an unreliable tail which needs to be truncated during generation and (3) Nucleus Sampling is currently the best available decoding strategy for generating long-form text that is both high-quality — as measured by human evaluation — and as diverse as human-written text.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://openreview.net/forum?id=rygGQyrFvH">The paper: The Curious Case of Neural Text Degeneration. Holtzman et al. ICLR 2020</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: The Curious Case of Neural Text Degeneration. Holtzman et al. ArXiv 2020](https://arxiv.org/abs/1904.09751)
  - [ICLR version: The Curious Case of Neural Text Degeneration. Holtzman et al. ICLR 2020](https://openreview.net/forum?id=rygGQyrFvH)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)

- For your information
  - [Beam Search - A Search Strategy on HACKERNOON](https://hackernoon.com/beam-search-a-search-strategy-5d92fb7817f)
  - [How to use Latex with latex4technics.com](https://www.latex4technics.com/?note=gw021j)
  - [MathJax on Stackexchange](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
