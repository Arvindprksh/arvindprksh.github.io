---
layout: post
title: What Is The Regular Expression
subtitle: The fundamental regular expression for some projects that need it
category: Natural Language Processing Labs
tags: [nlp, regular expression]
permalink: /2017-11-11/Regular_Expression/
css : /css/ForPDFShareByHyun.css
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

Whenever I am programming, I am confused about how to turn normal text into regular expression.

For practice of making regular expression, I decided to write blog about regular expression with frequent expression refered to by [8 Regular Exmpressions You Should Know](https://code.tutsplus.com/tutorials/8-regular-expressions-you-should-know--net-6149)

Let's start to explore about regular expression.

above all, Let's see Regular Expression E-mail Matching Example

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Regex.png)

### First, Matching a Username

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Matching_a_Username.png)

###### Pattern:

```
/^[a-z0-9_-]{3,16}$/
```
| Character | What does it do? | example | Matches |
| ^ | Matches begingin of line | ^abc | abc, abcdef..., abc123 |
| $ | Matches end of line | abc$ | my:abc, 123abc, theabc |
| [a-z] | Matches any characters between 'a' and 'z' | [b-z] | bc, mind, xyz |  
| {x, y} | Match between 'x' and 'y' times | (a){2,4} | aa, aaa, aaaaa |

###### Description:

We start by tellingthe parser of regular expression to fine the beginning of the string(^), followed by and lowercase letter(a-z), number(0-9), an underscore, or a hyphen. 

Next, {3, 6} Makes sure that are at least 3 of those characters, but no more than 16. Finally, We want the end of the string($).

###### String that matches:

 my-us3r_n4m3
 
###### String that doesn't match:

th1s1s-wayt00_l0ngt0beauername (too long)


### Second, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Password.png)

###### Pattern:

```
/^[a-z0-9_-]{6,18}$/
```

| Character | What does it do? | example | Matches |
| ^ | Matches begingin of line | ^abc | abc, abcdef..., abc123 |
| $ | Matches end of line | abc$ | my:abc, 123abc, theabc |
| [a-z] | Matches any characters between 'a' and 'z' | [b-z] | bc, mind, xyz |  
| {x, y} | Match between 'x' and 'y' times | (a){2,4} | aa, aaa, aaaaa |

###### Description:

Matching a password is very similar to matching a username. The only difference is that instead of 3 to 16 letters, numbers, underscore, or hyphens, we want 6 to 18 of them({6, 18})

###### String that matches:

myp4ssw0rd

###### String that doesn't match:

mypa$$w0rd (contains a dollar sign)

### Third, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Hex_Value.png)

###### Pattern:

```
/^#?([a-f0-9]{6}|[a-f0-9]{3})$/
```

| Character | What does it do? | example | Matches |
| ^ | Matches begingin of line | ^abc | abc, abcdef..., abc123 |
| $ | Matches end of line | abc$ | my:abc, 123abc, theabc |
| [a-z] | Matches any characters between 'a' and 'z' | [b-z] | bc, mind, xyz |  
| {x, y} | Match between 'x' and 'y' times | (a){2,4} | aa, aaa, aaaaa |
| ? | Matches the character before the ? zero or one times. Also, used as a non-greedy match | ab?c | ac, abc |
| || | OR operator | abc|xyz | abc or xyz |

###### Description:

We start by telling the parser of regular expression to find the beginning of the string(^). Next, a number sign is optional because it is followed a question mark. The question mark(?) tells the parser that the precedinng character - in this case a number sign(#)- is optional, but to be greedy and capture it if it's there.
Next, inside the first group(first group of parentheses), we can have two different situations. The first is any lowercase letter between **a** and **f** or **a number** six times.
The vertical bar tells us that we can also have three lowercase letters between **a** and **f** or **numbers** instead, Finally, we want the end of the string($)

The reason that I put the six character before is that parser will capture a hex value like #fffff. If I had reversed it so that three characters came first, the parser would only pick up #fff and not the other three f's

###### String that matches:

\#a3c113

###### String that doesn't match:

\#4d82h4 (contains the letter h)


### Fourth, Matching an E-mail

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/E-mail.png)

###### Pattern:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

| Character | What does it do? | example | Matches |
| ^ | Matches begingin of line | ^abc | abc, abcdef..., abc123 |
| $ | Matches end of line | abc$ | my:abc, 123abc, theabc |
| [a-z] | Matches any characters between 'a' and 'z' | [b-z] | bc, mind, xyz |  
| {x, y} | Match between 'x' and 'y' times | (a){2,4} | aa, aaa, aaaaa |
| ? | Matches the character before the ? zero or one times. Also, used as a non-greedy match | ab?c | ac, abc |
| || | OR operator | abc|xyz | abc or xyz |

###### Description:

###### String that matches:

###### String that doesn't match:


### Second, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Password.png)

###### Pattern:

```
/^[a-z0-9_-]{3,16}$/
```

###### Description:

###### String that matches:

###### String that doesn't match:


### Second, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Password.png)

###### Pattern:

```
/^[a-z0-9_-]{3,16}$/
```

###### Description:

###### String that matches:

###### String that doesn't match:


### Second, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Password.png)

###### Pattern:

```
/^[a-z0-9_-]{3,16}$/
```

###### Description:

###### String that matches:

###### String that doesn't match:


### Second, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Password.png)

###### Pattern:

```
/^[a-z0-9_-]{3,16}$/
```

###### Description:

###### String that matches:

###### String that doesn't match:


### Second, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Password.png)

###### Pattern:

```
/^[a-z0-9_-]{3,16}$/
```

###### Description:

###### String that matches:

###### String that doesn't match:


### Second, Matching a password

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2017-11-11-Regular_Expression/Password.png)

###### Pattern:

```
/^[a-z0-9_-]{3,16}$/
```

###### Description:

###### String that matches:

###### String that doesn't match:


# Reference 

 - [Regex](https://www.computerhope.com/jargon/r/regex.htm)

 - [8 Regular Exmpressions You Should Know](https://code.tutsplus.com/tutorials/8-regular-expressions-you-should-know--net-6149)  
