---
layout: post
title: 344. Reverse String (Difficulty-Eesy)
subtitle: Difficulty - Easy
category: LeetCode
tags: [algorithm, easy]
permalink: /2016/10/24/344_Reverse_String/
bigimg: 
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
---

# Agenda

I refered to [LeetCode](ttps://leetcode.com) site. 
  
From now on, I will practice sometimes. any time I practice, I will arrage what I do here

And clicking the title.(e.g Reverse String) makes you jump to problem page of Leetcode.

# [344. Reverse String](https://leetcode.com/problems/reverse-string/)
 
Write a function that takes a string as input and returns the string reveresd.

 - Example
  
  Given s = "hello", return "olleh"  

If you choose C language, Leetcode give you function format as follows. 

```c
char* reverseString(char* s) {

}
```

# My Solution


## 1. brute force

I just simply access this problem. 
  
-I verify the length of The given string
  
-based on the length, I reoder the string on another variable.
 
 The follow function is bases in C Languge
 
```c
char* reverseString(char* s) {
 
  int len = strlen(s);
  int count = 0; // index of new string 
  char* str = NULL;
  
  // In here, if input data is null, I have to return nothing. 
  if(len == 0)
    return "";
  else 
    str=(char*)malloc(sizeof(char)*(len+1);
    
  while (len != 0) {
    str[count++]=s[len-1];
    len--;
  }
  
  str[count]='\0';
    
  return str;
}
```

  Sometiemes, If you are confusing the allocation of memory between C and C++, Just Look at new and malloc one more time.
  
  the key difference is which on has construct and destruct
  
  i.e new operation call construct and destruct whenevet user generate and delete

---
 
*IF I have chance, I will arrange the above problem with another languge. For example, JAVA, C++ And so on* 


