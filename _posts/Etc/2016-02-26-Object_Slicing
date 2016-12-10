---
layout: post
title: Object Slicing
subtitle:
css:
tags:
date:
big-image:
share-image:
permalink:
comments:
show-share:
big-image:
meta-title:
meta-description:
---

간단히 말해서 객체가 잘리는 현상이 발생을 하는데 그것은 

<pre>
<code>
class AAA
{
  .......
}

class BBB : public AAA
{
}

// 객체잘림

  AAA a;
  BBB b;
  
  a = b; // 바로 이부분에서 객체가 잘림 현상이 발생

</code>
</pre>

즉 위에서 볼수 있듯이 객체가 잘림 현상은 부모 객체에 자식 객체를 대입할려고 할 때 발생한다. 
