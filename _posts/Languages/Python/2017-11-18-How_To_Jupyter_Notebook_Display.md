---
layout: LatexPostByHyun
title: How To Jupyter Notebook Display 
subtitle: The primary target is latex. 
category: Python
tags: [latex, jupyter notebook]
permalink: /2017/11/18/How_To_Jupyter_Notebook_Display/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

If you use jupyter notebook. in particular with deep learing and machine learning. you need some mathematical sign to note in jupyter noteboke.

Then, I recommend you to use latex, which helps you write those signs in jupyter notebook or HTLM page. 

The basic way to use latex is **$$** as start and end mark like this 

```
$$c = \sqrt{a^2 + b^2}$$
```

$$c = \sqrt{a^2 + b^2}$$

And another way is **%%** sign

```
%%latex
\begin{align}
\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} & = \frac{4\pi}{c}\vec{\mathbf{j}} \\
\nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\
\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\
\nabla \cdot \vec{\mathbf{B}} & = 0
\end{align}
```

%%latex
\begin{align}
\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} & = \frac{4\pi}{c}\vec{\mathbf{j}} \\
\nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\
\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\
\nabla \cdot \vec{\mathbf{B}} & = 0
\end{align}



# Reference 

 - [Stackoverflow](https://stackoverflow.com/questions/13208286/how-to-write-latex-in-ipython-notebook)

 - [jupyter notebooke's an example](http://nbviewer.jupyter.org/github/ipython/ipython/blob/2.x/examples/Notebook/Display%20System.ipynb#LaTeX)
 
 Appendix for MathJax:
 
 - [The jekyll Extras](https://jekyllrb.com/docs/extras/)
 
 - [How to use MathJax in jekyll](http://www.gastonsanchez.com/visually-enforced/opinion/2014/02/16/Mathjax-with-jekyll/ )
 
 
