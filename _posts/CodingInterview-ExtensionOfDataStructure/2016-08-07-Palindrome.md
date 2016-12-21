---
layout: post
title: What is the palindrome ?
subtitle: How to resolve the palindrome below 
category: Extenstion Of DataStructure
tags: [stack, algorithm]
permalink: /2016/08/07/Palindrome/
---

# Palindrome 

  what is the Palindrome? 
  
  if there is a word, ababXbaba. In this time. people call that word palindrome. 
  
  that is, reading a word from end to front is equal to reading a word from front to end.
  
  a couple of days ago. you use the linked list and stack, and with that, we designed the algorithm.
  
  today, now just If the ababXabab is in the array. 
  
  So then, you will check if the above word is palindrome.
  
  the easiest way is to start comparison from both end. 
  
  for example, one starting point is first letter. the other one is last letter.
  
  1 ) increasing stating point 
  
  2 ) decreasing last point, until meet both two point. 
  
  3 ) continue comparing those things until starting point < last point.
   
```
starting point last point.  
  | ->         <- |  
  a b a b X b a b a.  
```
  
  let's make simple code. 
  
  Especailly, just the above letter is standard of the following code.
  
  the following is middle of string is always X. 

```c
  int IsPalindrome(char * A) {
   int i = 0, j = strlen(A)-1;
   
   while (i < j && A[i] == A[j]) {
      i++;
      j--;
   }
   
   if (i < j) {
      printf("this string is not plaindrome\n");
     return 0;
   }
   else {
      printf("this string is plaindrome\n");
      return 1;
   }
  }
```
  
## If string is linked list or you use the stack. how do you solve this problem ??

  If you want to know, just click [this site](./Extension_Of_Data_structure/2016-08-03-Finding_If_a_singly_Linked_list_is_palindrome)
  
  
### Stack 

  In the case of using the stack, the algorithm is as follows.

##### My algorithm. 

  This algorithme is very simple. just use the stack. 
  
  First of all, put all string on top of stack in order.
  
  Second of all, popping the top of stack, you compare the popped item and the original string. but string starts in front. 
  
  Third of all, all string is the same, this string is palindrome.
  
  let's see pseudo code. 
  
```c
  void Ispalindrome(struct Stack * s, char * d) {
      int len = strlen(d);
      
      for (int i = 0 ; i < len ; i++) {
          s.push(d[i]); // push one of string on top of stack. 
      }
      
      // after the above push. 
      
      for (int i = 0 ; i < len ; i++) {
        
        if ( compare(s.pop(). d[i]) ) // if both is same, this for statement continues
            continue;
        else {
            printf("this string is not palindrome\n");
            break; 
         }
      }
  }
```

But let's think of another way to introduce in coding book. 


### Another way. 

  In this case, ababXbaba. you don't have to compare all the string.
  
  just you have to do by 'X' letter. 
  
  So the algoritm that coding book introduce is as follows. 
  
  First of all, you have to searching for string until meeting 'x' letter. 
  
  Second of all, at the same time, you have to push one of string you are searching on the top of stack. 
  
  Third of all, after meeting the 'x' letter in orginal string. you have to compare top of stack with the rest of the string. 
  In this time. the top of stack and one of string is the same. then this string is palindrome.
  
  three process above is repeated, until stack is empty. 
  
  let's make pseudo code 
  
  This following pseudo code is my thought. 
  
```c
  void IsPalindrome(char * d, struct Stack *s) {
    int len = strlen(d);
    int locationOfX = 0  
    int i ;
    // in .cpp file, if I use the file with C grammar. 
    for (i = 0 ; i < len && d[i] != 'x' ; i++) {
        s.push(d[i]);     
    }
    locationOfx = i;
    
    for ( i = locationOfX ; i < len ; i++) {
      
          if (d[i] != s.pop()) {
              printf("this string is not palindrome\n");
              return; 
          }
    }
  }
```
  
  Now, Just compare the above code with code of coding interviewing book. 
  
  let's follow the cod of the book. 
  
```c
  int IsPalindrome(char * A) {
      int i = 0; 
      struct Stack S=createStack();
      
      while(A[i] != 'x') {
          Push(S, A[i]);
          i++;
      }
    
      i++;
      
      // the end of string in c language is '\0' So You can use this. 
      While(A[i]) {
          if(IsEmptyStack(S) || A[i] != Pop(s)) {
              printf("Not a Palindrome");
              return 0;
          }
          
          i++;
      }
      
      return IsEmptyStack(S); // here show you if the stack is empty.
  }
```
  
If you want to know and practice palindrome, visit [Leetcode's Longest-plaindrome-substring](https://leetcode.com/problems/longest-palindromic-substring/)

