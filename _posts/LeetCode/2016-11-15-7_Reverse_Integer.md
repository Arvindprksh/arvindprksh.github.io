---
layout: post
title: 7. Reverse Integer
subtitle: Difficulty - Easy
category: LeetCode
tags: [algorithm, c function, easy]
permalink: /2016/11/15/7_Reverse_Integer/
bigimg: 
    - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
---

# [7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

Reverse digits of an Integer.

Example1 : x = 123 , return 321

Example2 : x = -123 , return -321

```c
int reverse(int x) {
    
}
```

# My Solution 

 - just % and * with 10 

```c
int reverse(int x) {
    int digit=10;
    int number=x;
    int returnNumber = 0;

    while (number != 0 ) {
        if (returnNumber * 10/10 != returnNumber)
            return 0;
        returnNumber *=10;
        returnNumber += number%10;
        number = number/10;
    }

    return returnNumber;
    
}
```

  I wanted to change a part of the above source. 
  
```c
int reverse(int x) {
    int digit=10;
    long long int number=x;
    long long int returnNumber = 0;

    while (number != 0 ) {
        if ((returnNumber * 10 > INT_MAX) || (returnNumber * 10 < INT_MIN))
            return 0;
        returnNumber *=10;
        returnNumber += number%10;
        number = number/10;
    }
    return returnNumber;
}
````

# Reference

on C++, headerfile including INT_MIN, INT_MAX is <climits>
