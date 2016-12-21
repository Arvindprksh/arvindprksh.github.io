---
layout: post
title: how long is the rotation of linkedList ? 
subtitle: If Your LinkedList has rotation, How Long is the rotation ??
category: Extenstion Of DataStructure
tags: [list]
permalink: /2016/07/08/Utilization_Of_LinkedList3/
---

# Check If list is Loop, and then if Loop is right, what is the length of loop ???

    how to solve this problem 
     
 > 1. I think that I have to check Loop with floyd finding cycle algorithm.   
 > 2. I think that I have to find the beginning of loop   
 > If you want to skip 2, just slowNode is placed in beginning of list, again you have to move slowNode to fastNode   
 > In this time, distance of moving slowNode is the length of loop   
 >
 
```c
 int FindBeginningOfLoop (struct ListNode * head) {
    struct ListNode * fastnNode = head, slowNode = head;
    int loopExits = 0
    
    while ( fastNode != NULL && slowNode != NULL) {
      
      fastNode = fastNode -> next;
      
      if (fastNode == slowNode) {
       loopExits = 1;
        break;
      }
      
      if (fastNode == NULL)
          break;
      fastNode = fastNode -> next;
      
      if (fastNode == slowNode) {
       loopExits = 1;
        break;
      }
      slowNode = slowNode -> next;
    }
    
    if (loopExits == 1) {
        int count =0;
        slowNode = head; // or I only have to move slowNode without chang head.
        
        while (slowNode == fastNode) {
           count++;
           slowNode = slowNode -> next;
        }
        
        return count;
    }
    
    return 0;
 }
```
