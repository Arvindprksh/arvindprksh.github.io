---
layout: post
title: 8. String to Integer(atoi)
subtitle: Difficulty - Easy
category: LeetCode
tags: [algorithm, easy]
permalink: /2016/11/26/8_String_To_Integers(atoi)/
bigimg: 
    - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# [8. String to Integer(atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

Implement atoi to covert a string to integer.

Hint  : Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input case.

 i.e If you want to see hint, just click title. You can get hint from original site of leetcode.

Notes : It is inteded for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

```c
int myAtoi(char* str) {
    
}
```

# My Solution. 

 The following is assumption of input cases. 
 
 - if the string includes characters except for number character. 
 
 - if string first includes minus sign. in this case, I have to deal with this string to negative number.  


```c
int myAtoi(char* str) {
   int sign = 1,  digit = 10;
   long int returnValue = 0; 
   int i=0; 
   
   // where is the starting point of number ?
   while (str[i] == ' ') {
         i++;
   }
   
   // check if the number is negative or positive ?
   if (str[i] == '-' || str[i] == '+') {
        sign = (str[i] == '-') ? -1 : 1;
        i++;
   }
   
   // check if the range of number is between INT_MAX and INT_MIN  ?
   while ( '0' <= str[i] && str[i] <= '9') {
      
      returnValue = returnValue*10 + (long int)(str[i] - '0');
      
      if(returnValue*sign >= INT_MAX){
               return INT_MAX;
      }
      else if (returnValue*sign <= INT_MIN) {
               return INT_MIN;
      }
      i++;
   }
   
   return returnValue*sign;
}
```
