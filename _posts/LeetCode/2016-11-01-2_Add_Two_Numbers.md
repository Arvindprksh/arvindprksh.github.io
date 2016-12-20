---
layout: post
title: 2. Add Two Numbers
subtitle: Difficulty - Medium
category: LeetCode
tags: [algorithm, medium]
permalink: /2016/11/01/2_Add_Two_Numbers/
bigimg: 
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
---


# [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
 
You are given two linked lists representing two non-negative numbers. the digits are stored in reverse order and each of their nodes contain a single digit, Add the two numbers and return it as a liked list.

 - Example
 
  Input : (2 -> 4 -> 3) + (5 -> 6 -> 4)
  
  output : 7 -> 0 -> 8 
  
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
    
}
```

# My Solution. 

 1. brute force.
 
  -  I don't know which one is longer, so at first, we have to konw length of each list. 
  -  liek merge sort, jut add them. 
 
 
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
    
    struct ListNode *sum=null; 
    struct ListNode *firstNode=null; // for return 
    struct ListNode *temp = l1;  // for length
    int flag =0;
    
    int countl1=0;
    int countl2=0;
    
    while (temp != 0) {
      countl1++;
      temp = temp -> next;
    }
    
    temp = l2;
    
    while (temp !=0 {
      countl2++;
      temp = temp -> next;
    }
    
    if (countl1 > countl2) {
      sum = (struct ListNode *)malloc(sizeof(struct ListNode));
      firstNode = sum;
    }
    
    while (l1 || l2) {
      int temp = l1->val + l2->val + flag;
      flag =0;
     
      if (temp >= 10) {
         flag = temp/10;
         temp = temp%10;
      }
      
      sum -> val = temp;
      sum = sum -> next;
     
      l1 = l1 -> next;
      l2 = l2 -> next;
    }
    
    if (l1 != null) {
      while (l1 != null) {
         
         
         if (flag == 1) {
          
         }
  
      }
    }
    else if (l2 != null){
      while (l2 != null) {
        
         if (flag == 1) {
           
         }
      
      }
    }
    else if (l1 == null && l2 == null) {
    
    }
   
    return sum; 
}
```

- as you can see the above code, it's too much, I think I need to chang my algorithm. 

- when I look at the discusiion of this problem on Leetcode site, people is suprisin, 
 
- they can consider more efficient way to reach the solution 

 2. like the actual addition. 
 
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
  struct ListNode * current = (struct ListNode *)malloc(sizeof(struct ListNode));
  struct ListNode * firstNode = current;
  struct ListNode *test1=l1, *test2=l2;
  int flag =0;
  
  current -> val = 0;
  current -> next =NULL;
  
  while (test1 != NULL || test2 != NULL || flag ) {
    current -> val = flag; 
    
    if (test1 != NULL) {
      current -> val += test1 -> val;
      test1 = test1 -> next;
    }
    
    if (test2 != NULL) {
      current -> val += test2 -> val;
      test2 = test2 -> next;
    }
    
    if (current -> val >= 10) {
      flag = current->val / 10;
      current -> val = current -> val % 10;
    }
    else 
      flag = 0;
      
    if (test1 != NULL || test2 != NULL || flag > 0) {  
     current -> next = (struct ListNode *)malloc(sizeof(struct ListNode));
     current = current -> next;
     current -> val = 0; 
     current -> next = NULL;
    }
  }
  return firstNode;
}
``` 
 
 I realized that I must initialize each variable on Leetcode, if you do not that. you get error message like runtime error.
 
 3. finall solution is that of LeetCode
 
  - this solution is similar to my solution but code is more simple. 
  
  - I think LeetCode's solution is intuitive and time to solve this problem is the same. 
  
  - On LeetCode, They explain that with JAVA, But In here I will chage the code to C Language.
  
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
  struct ListNode * current = (struct ListNode *)malloc(sizeof(struct ListNode));
  struct ListNode * firstNode = current;
  struct ListNode *test1=l1, *test2=l2;
  int flag =0;  
  
  current -> val = 0;  // OR   // current -> val = 0;
  current -> next =NULL; // OR  // current -> next =NULL;
  
  while (test1 != NULL || test2 != NULL) {
     int x = (test1 != NULL) ? test1 -> val : 0;
     int y = (test2 != NULL) ? test2 -> val : 0;
     int sum = flag + x + y;
     flag = sum/10;
     current-> next = (struct ListNode *)malloc(sizeof(struct ListNode));
     current = current -> next;
     current -> val = sum%10;
     current -> next = NULL;
     
     if (test1 != NULL) 
        test1 = test1-> next;
     if (test2 != NULL)
        test2 = test2 -> next;
  }
  
  if (flag > 0) {
     current-> next = (struct ListNode *)malloc(sizeof(struct ListNode));
     current -> next -> val = flag;
     current -> next -> next = NULL;
  }
  
   return firstNode->next;
 }
```
