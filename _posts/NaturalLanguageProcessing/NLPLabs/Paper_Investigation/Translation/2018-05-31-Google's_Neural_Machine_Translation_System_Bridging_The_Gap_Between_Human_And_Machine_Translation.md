

While I have studied for Korean Natural Language processing about Neural Network. I was finding the architecture for my work. 

So I read this paper and I realized about dealing with a seqeunce of data. 

This paper is end-to-end model for Neural Network translation. In my case, I wondered the architectur of neural network about how to use LSTM for translation. 

I was inspired from this paper. 

Their basic architecture of neural network translation : 

encoder, attention mechanism, and decoder. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2018-05-31-Google-s_Neural_Machine_Translation_System-_Bridging_The_Gap_Between_Human_And_Machine_Translation/Google_Neural_Network_Translation1.JPG)

Also they used residual connection like this:

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2018-05-31-Google-s_Neural_Machine_Translation_System-_Bridging_The_Gap_Between_Human_And_Machine_Translation/Google_Neural_Network_Translation2.JPG)


plus, For feature generation as vector, they used Bi-directional LSTM considering long and short dependancy from output.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2018-05-31-Google-s_Neural_Machine_Translation_System-_Bridging_The_Gap_Between_Human_And_Machine_Translation/Google_Neural_Network_Translation3.JPG)

except for thing above, they said for computational speed, they used parallelism to each layers. 

But I am goning to go through in detail here, 


Another problem, in particular, of NLP is out-of-vocabulary. i.e. rare word is trouble in open vocabulary system. 

In the case of theirs, they used sub-word units like wordpiece model. 

{% highlight linenos %}
• Word: Jet makers feud over seat width with big orders at stake
• wordpieces: _J et _makers _fe ud _over _seat _width _with _big _orders _at _stake
{% endhighlight %}

**\_** sign is special mark for the beggining of a word. 


If you want to know detail, read 4 section, Segmentation Approaches.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
This paper explained Neural Machine Translation(NMT). it is an end-to-end learning approach for automated translation with the potential to overcome many of the weaknesses of conventional phrased-based translation systems.
The architecture of it comprises encoder, attention mechanism, and decoder. The reminder about this article used bidirectional LSTM(long-short term memory) for feauture generation.
And the connection between encoder and decoder is attention mechanism is responsible for it. They say, in their experience of translation task with large-scale data,  the number of layer of lstm works well up to 4 layers, barely with 6 layers and very poorly beyond 8 layers.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1609.08144v2">The paper: Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation</a>
</div>

# Reference 

- [OPentNMT](http://opennmt.net/OpenNMT/training/models/)

- Paper 
  - [Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation](https://arxiv.org/abs/1609.08144v2)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
 
