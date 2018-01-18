---
layout: post
title: Font Awesom class inside a Bootstrap alert.
subtitle: How to use icon in HTML.
category: Web Programming
tags: [Bootstrap, html]
permalink: /2018/01/18/Bootstrap_alert/
css :  "/css/ForYouTubeByHyun.css"
bigimg: 
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
---

In the theme of html, you want to chagne font or icon. Look at this site, [Font Awesome library](http://fontawesome.io/icons/) to see the available icons.

The Font Awesome icons allow you to adjust their size by adding **fa-2x**, **fa-3x** and so forth as a class to the icon to adjust their size to two times or three times original size

let's see an simple example with <i class="fa fa-paperclip"></i>

# attach icon <i class="fa fa-paperclip"></i>

```html
<i class="fa fa-papercli"></i> normal size (1x)
<i class="fa fa-papercli fa-lg"></i> fa-lg
<i class="fa fa-papercli fa-2x"></i> fa-2x
<i class="fa fa-papercli fa-3x"></i> fa-3x
<i class="fa fa-papercli fa-4x"></i> fa-4x
<i class="fa fa-papercli fa-5x"></i> fa-5x
```

<i class="fa fa-papercli"></i> normal size (1x)
<i class="fa fa-papercli fa-lg"></i> fa-lg
<i class="fa fa-papercli fa-2x"></i> fa-2x
<i class="fa fa-papercli fa-3x"></i> fa-3x
<i class="fa fa-papercli fa-4x"></i> fa-4x
<i class="fa fa-papercli fa-5x"></i> fa-5x

# alert :  <div class="alert alert-danger" role="alert"><i class="fa fa-exclamation-circle"></i> <b>Warning: </b>This is a special warning message.</div>


Note : 

```html
<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b> Add your note here </div>
```
<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b> Add your note here </div>

---

Tip : 

```html
<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b> Add your tip here </div>
```
<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b> Add your tip here </div>

---

important : 

```html
<div class="alert alert-warning" role="alert"><i class="fa fa-warning"></i> <b>Important: </b> Add your important here </div>
```
<div class="alert alert-warning" role="alert"><i class="fa fa-warning"></i> <b>Important: </b> Add your important here </div>

---

warning : 

```html
<div class="alert alert-danger" role="alert"><i class="fa fa-exclamation-circle"></i> <b>Warning: </b> Add your warning here </div>
```
<div class="alert alert-danger" role="alert"><i class="fa fa-exclamation-circle"></i> <b>Warning: </b> Add your warning here </div>

# Reference 

 - [icon of jekyll Doc Theme 6.0](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
