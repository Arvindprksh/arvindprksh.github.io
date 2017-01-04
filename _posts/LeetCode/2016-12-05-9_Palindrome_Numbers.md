---
layout: post
title: 9. Panlindrome Number
subtitle: Difficulty - Easy
category: LeetCode
tags: [algorithm, easy]
permalink: /2016/12/05/9_Palindrome_Numbers/
bigimg: 
    - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
---

# [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

Determine whether an interger is a palindrome. Do this without extra space. 


```c
bool isPalindrome(int x) {
    
}
```

# My Solution

 First, reverse the x. 
 
 Second, compare the reverse one with the original number. 
 
 Let's see my code 

```c
bool isPalindrome(int x) {
    int copyOfX=x;
    int reverseNumber = 0;
    int flag=0; // first digit from right side. 
    
    if (x < 0) // I found that negative number is not always palindrome in here site.  
        return false;
    
    if (x < 10) // this means if digit of number is one, that is always palindrome
        return true;

    // from now on, I will reverse x to compare the original number with the reverse number.

    // first, reverse the number(x)
    while (copyOfX != 0){
        
        int temp = copyOfX%10;
        
        if (flag == 0)
            flag =1;   
        else 
            reverseNumber *= 10;
       
        reverseNumber += temp; 
        
        copyOfX /= 10;
        
        //for debugging in leetcode site. 
        //printf("copyOfX : %d, reverseNumber : %d\n", copyOfX, reverseNumber);
    }
    
    // second, compare the original to the reverse thing
    if (x == reverseNumber)
        return true;
    else
        return false;
}
```

# Another Solution of the above one 

I thought I just wanted to reduce one of my code line.

So I could find out one, that is flag variable. 

Because I think when I make a code, if I have many turning point variables. 

it is not easy to understaning the logic of code. 

that is just my thought, If you have another one, Just say to me. I would like to discuss about it.

let's see how to shrink my code lines. 

```c
bool isPalindrome(int x) {
    int copyOfX=x;
    int reverseNumber = 0; 
    
    if (x < 0) // I found that negative number is not always palindrome in here site.  
        return false;
    
    if (x < 10) // this means if digit of number is one, that is always palindrome
        return true;

    // from now on, I will reverse x to compare the original number with the reverse number.

    // first, reverse the number(x)
    while (copyOfX != 0){
        
        reverseNumber = reverseNumber*10 + copyOfX%10;
       
        copyOfX /= 10;
        
        //for debugging in leetcode site. 
        //printf("copyOfX : %d, reverseNumber : %d\n", copyOfX, reverseNumber);
    }
    
    // second, compare the original to the reverse thing
    if (x == reverseNumber)
        return true;
    else
        return false;
}
```
 
