---
layout: post
title: 9. Panlindrome Number
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

# [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

Determine whether an interger is a palindrome. Do this without extra space. 

```c
bool isPalindrome(int x) {
    
}
```
# Solution

in my case, I got hint form this problem site. 

  1. x is integer, so it take a little time to reverse a number. 
  
  2. negative nubmer is not palindrome  -> I could test that in Leetcode. so I could know this. 
  
  3. x is 0,rather, if digit is one, tha number is palindrome.

```c
bool isPalindrome(int x) {
    int reverseNumber = 0; 
    int temp = x;
    int i=0;
    if (temp < 0 || (temp!= 0 && (temp%10 < 10)))
        return false;
    
    while ( temp != 0 ) {
        reverseNumber = reverseNumber*(10*i) + temp%10;
        temp /= 10; 
        i++;
    }
    
    return (reverseNumber == temp);
}
```

