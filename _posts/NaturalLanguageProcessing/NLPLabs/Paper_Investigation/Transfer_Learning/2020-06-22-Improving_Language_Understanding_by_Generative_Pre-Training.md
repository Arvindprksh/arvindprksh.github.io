---
layout: post
title: Improving Language Understanding by Generative Pre Training
subtitle: Title of paper - Improving Language Understanding by Generative Pre Training
category: NLP papers - Transfer Learning
tags: [transfer learning]
permalink: /2020/06/22/Improving_Language_Understanding_by_Generative_Pre-Training/
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

This is a brief summary of paper for me to study and organize it, [Improving Language Understanding by Generative Pre-Training. Radford et al. 2018](https://paperswithcode.com/paper/improving-language-understanding-by) I read and studied. 
{% include MathJax.html %}

This paper focus on transfer learning with generative pre-training. 

They also proposed task-agnostic model as follows:

When they used lagnauge modeling as pre-training objective and then fine-tunes model on target task with auxiliary training objective, which is language modeling.

![Radford et al. 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Transfer_Learning/2020-06-22-Improving_Language_Understanding_by_Generative_Pre-Training/task-agnostic_model.PNG)

To sum up, 

Leveraging more than word-level information from unlabeled text, however, is challenging for two main reasons. 

First, it is unclear what type of optimization objectives are most effective at learning text representations that are useful for transfer. Recent research has looked at various objectives such as language modeling, machine translation, and discourse coherence, with each method outperforming the others on different tasks.

Second, there is no consensus on the most effective way to transfer these learned representations to the target task. 

Existing techniques involve a combination of making task-specific changes to the model architecture, using intricate learning schemes and adding auxiliary learning objectives. 

These uncertainties have made it difficult to develop effective semi-supervised learning approaches for language processing.

For their model architecture, they use the Transformer, which has been shown to perform strongly on various tasks such as machine translation, document generation, and syntactic parsing.

This model choice provides us with a more structured memory for handling long-term dependencies in text, compared to alternatives like recurrent networks, resulting in robust transfer performance across diverse tasks. 

During transfer, they utilize task-specific input adaptations derived from traversal-style approaches, which process structured text input as a single contiguous sequence of tokens.

As they demonstrate in our experiments, these adaptations enable us to fine-tune effectively with minimal changes to the architecture of the pre-trained model.

They evaluate our approach on four types of language understanding tasks – natural language inference, question answering, semantic similarity, and text classification. 

Their general task-agnostic model outperforms discriminatively trained models that employ architectures specifically crafted for each task, significantly improving upon the state of the art in 9 out of the 12 tasks studied. 

They also analyzed zero-shot behaviors of the pre-trained model on four different settings and demonstrate that it acquires useful linguistic knowledge for downstream tasks.

**Semi-supervised learning for NLP** 

>>Their work broadly falls under the category of semi-supervised learning for natural language. This paradigm has attracted significant interest, with applications to tasks like sequence labeling or text classification.   
>>The earliest approaches used unlabeled data to compute word-level or phrase-level statistics, which were then used as features in a supervised model.   
>>Over the last few years, researchers have demonstrated the benefits of using word embeddings, which are trained on unlabeled corpora, to improve performance on a variety of tasks. These approaches, however, mainly transfer word-level information, whereas they aim to capture higher-level semantics.    
>>Recent approaches have investigated learning and utilizing more than word-level semantics from unlabeled data. Phrase-level or sentence-level embeddings, which can be trained using an unlabeled corpus, have been used to encode text into suitable vector representations for various target tasks.  
>>Unsupervised pre-training Unsupervised pre-training is a special case of semi-supervised learning where the goal is to find a good initialization point instead of modifying the supervised learning objective.   
>>Early works explored the use of the technique in image classification and regression tasks.     
>>Subsequent research demonstrated that pre-training acts as a regularization scheme, enabling better generalization in deep neural networks.   
>>In recent work, the method has been used to help train deep neural networks on various tasks like image classification, speech recognition, entity disambiguation and machine translation.  
>>The closest line of work to ours involves pre-training a neural network using a language modeling objective and then fine-tuning it on a target task with supervision.  
>>Although the pre-training phase helps capture some linguistic information, their usage of LSTM models restricts their prediction ability to a short range. In contrast, our choice of transformer networks allows us to capture longerrange linguistic structure, as demonstrated in their experiments.  
>>Further, we also demonstrate the effectiveness of our model on a wider range of tasks including natural language inference, paraphrase detection and story completion.  
>>Other approaches use hidden representations from a pre-trained language or machine translation model as auxiliary features while training a supervised model on the target task.
>>This involves a substantial amount of new parameters for each separate target task, whereas they require minimal changes to our model architecture during transfer.   
>>Auxiliary training objectives Adding auxiliary unsupervised training objectives is an alternative form of semi-supervised learning.  

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Natural language understanding comprises a wide range of diverse tasks such as textual entailment, question answering, semantic similarity assessment, and document classification. Although large unlabeled text corpora are abundant, labeled data for learning these specific tasks is scarce, making it challenging for discriminatively trained models to perform adequately. They demonstrate that large gains on these tasks can be realized by generative pre-training of a language model on a diverse corpus of unlabeled text, followed by discriminative fine-tuning on each specific task. In contrast to previous approaches, they make use of task-aware input transformations during fine-tuning to achieve effective transfer while requiring minimal changes to the model architecture. They demonstrate the effectiveness of their approach on a wide range of benchmarks for natural language understanding.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://paperswithcode.com/paper/improving-language-understanding-by">The paper: Improving Language Understanding by Generative Pre-Training. Radford et al. 2018</a>
</div>

# Reference 

- Paper 
  - [Paperswithcode: Improving Language Understanding by Generative Pre-Training. Radford et al. 2018](https://paperswithcode.com/paper/improving-language-understanding-by)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [Improving Language Understanding with Unsupervised Learning on OpenAI blog](https://openai.com/blog/language-unsupervised/)
  - [The Blurry Lines of Supervised and Unsupervised learning on Towards Data Science blog](https://towardsdatascience.com/the-blurry-lines-of-supervised-and-unsupervised-learning-b8a2aa04c8b0)
  - [Self-Supervised Representation Learning on Lil'Log](https://lilianweng.github.io/lil-log/2019/11/10/self-supervised-learning.html)































