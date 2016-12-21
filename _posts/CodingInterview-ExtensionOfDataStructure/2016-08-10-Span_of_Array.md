---
layout: post
title: How to measure span of A[j] <= A[i] of a array 
subtitle: In an given array,A[i], when A[j] <= A[i], what is the range of maximum of j-i 
category: Extenstion Of DataStructure
tags: [stack]
permalink: /2016/08/10/Span_of_Array/
---

Article of Extennsion of Data Structure base in geeksforgeeks and my Coding Interview Question.

But, mainly, I quote Coding Interview Question book first. Next, I look for GeeksforGeeks site to find out a similar thing. 

This article that I practice for thought of algorithm.  

# Problem 

## The Stock Span Problem

![](/img/Image/CodingInterview-ExtensionOfDataStructure/2016-08-10-Span_of_Array/Span_of_Stock.png)

The following article quote this [GeeksforGeeks](http://www.geeksforgeeks.org/the-stock-span-problem/) 

As You can see the above figure, The stock span problem is a financial problem where  we have a series of n daily price quotes for a stock and we need to calculate span of stock's price for all n days. 

The span Si of the stock's price on a given day i is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the current day is less than or equal to its prices on the given day. For example, if an array of 7 days prices is given as {100, 80, 60, 70, 60, 75, 85}, then the span values for corresponding 7 days are {1, 1, 1, 2, 1, 4, 6}

# Algorithm 

## Brute force 

Traverse the input price array, For every element visited, traverse elements on left of a given day and increase the span value of it while elements on the left side are smaller. 

 1. you have to use two of for statements. first is the total length, and second is the number of left side until meeting a less thing than price of a given day.  

```c++
// you have to fill s[] with span values.
void calculateSpan(int price[], int n, int s[]) {

  memset(s, 0, sizeof(s));
  
  for (int i = 0 ; i < n ; i++) {
    for(int j = i ; j > -1 ; j--) {
      if ( price[i] >= price[j] ) 
          s[i]++;
    }
  }
}
```
the algorithm is the same from above. 

BUT making code is different a little. 

The following is on GeeksforGeeks

```c++
// Fills array s[] with span values
void calculateSpan(int price[], int n, int s[]){
 
  // Span value of first day is always 1. 
  s[0] = 1; 
  
  // Calculate span value of remaining days by linearly checking previous days. 
  for (int i = 1 ; i < n ; i++) {
    s[i] = 1; // Initilize span value. 
    
    // Traverse left while the next element on left is smaller than price[i]
    for (int j = i -1 ; ( j >= 0) && (price[i] >= price[j]) : j--)
      s[i]++;
  }
}
```

The above method is O(n^2). because of two times of for statement 

 2. you can improve the above case, 
  
```c++





```
 
# Reference 

 [GeeksforGeeks](http://www.geeksforgeeks.org/the-stock-span-problem/)
