---
layout: post
title: 3. Longest substring without Repeating characters
subtitle: Difficulty - Medium
category: LeetCode
tags: [algorithm, c function, medium]
permalink: /2016/11/02/3_Longest_Substring_Without_Repeating_characters/
bigimg: 
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
---

# [3. Longest substring without repeating characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string, find the length of the longest substring without repeaing characaters. 

  - Example 
    
     - Given **"abcabcbb"**, the answer is **"abc"**, which the length is 3. 
     
     - Given **"bbbbb"**, the answer is **"b"**, with the length of 1. 
     
     - Given **"pwwkew"**, the answer is **"wke"**, with the length of 3. Note that the answer must be a substring, 
     
     **"pwke"** is a subsequence and not a substring.  
     
```c
int lengthOfLongestSubstring(char* s) {
    
}
```
  
# My solution

## 1. Brute force - with hash

  - First of all, I use the  of for statement. First is just for length of substring. Second is just for index of the original string, Third is for checking if there is the same thing in substring. (pre-requisit is just english and lony lowercase).
   * but, this problem include the special charaters. So you consider range of ASCII code
  
```c
// a b c d e f g h i  j  k  l  m  n  o  p  q  r  s  t  u  v  w  x  y  z
// 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26
int lengthOfLongestSubstring(char* s) {
   int i =0, j=0, k=0;
   char alphabets[128];
   int flag = 0; 
  
   // the length of substring
   for ( i = 0 ; i < strlen(s) ; i++) {
      // for original string's index
      for ( j = 0 ; j < strlen(s) ; j++) {
           int tag=0;
           // not over the whole string. 
           if (j + i >= strlen(s))
                break;
                
           // for initializaion of temp array
           memset(alphabets, 0, sizeof(alphabets));
           
           for (k = j ; k < j+i+1 ; k++) {
              int index = (s[k])%128;
              
              if ( alphabets[index] == 0 )
                    alphabets[index] = 1;
              else{ 
                  tag = 1;
                  break;
              }
           }
           
           if ( tag == 0 ) {
              flag = i+1;
           }
      }
   }
   return flag;
}
```
After testing with the above code. the result is Time Limit Exceeded.

## 2. brute force with reverse order + hash 

  - the point of the above problem is for the longest charaters. so I will try this function with reverse order
  
```c
// a b c d e f g h i  j  k  l  m  n  o  p  q  r  s  t  u  v  w  x  y  z
// 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26
int lengthOfLongestSubstring(char* s) {
   int i =0, j=0, k=0;
   char alphabets[128];
   int flag = 0; 
  
   // the length of substring
   for ( i = strlen(s) ; i > 0 ; i--) {
      // for original string's index
      for ( j = 0 ; j < strlen(s) ; j++) {
           int tag=0;
           // not over the whole string. 
           if (j + i > strlen(s))
                break;
                
           // for initializaion of temp array
           memset(alphabets, 0, sizeof(alphabets));
           
           for (k = j ; k < j+i ; k++) {
              int index = (s[k])%128;
              
              if ( alphabets[index] == 0 )
                    alphabets[index] = 1;
              else{ 
                  tag = 1;
                  break;
              }
           }
           
           if ( tag == 0 ) {
              flag = i;
              return flag;
           }
      }
   }
   return flag;
}
```
In this case, Time Limit exceeded. 

# Another way

  I think sliding is best way, this means just from where substring is wrong, just restart !!
  
  For example, 
  
  -> a b c a b c b b 
  
  -> a b c **a**
  
  -> then You have to check if location of **a** is in in a b c.   

```c
// a b c d e f g h i  j  k  l  m  n  o  p  q  r  s  t  u  v  w  x  y  z
// 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26
int lengthOfLongestSubstring(char* s) {
   int i =0;
   unsigned char alphabets[128] = {-1};
   int maxlen = 0, currentlen = 0;
   
   for ( i = 0 ; i < strlen(s) ; i++) {

       if (alphabets[s[i]] != -1) {
            i = alphabets[s[i]];
            memset(alphabets, -1, sizeof(alphabets));
            currentlen = 0; 
            continue;
       }
       alphabets[s[i]] = i;
       maxlen = ( maxlen > ++currentlen ) ? maxlen : currentlen; 
   }
   return maxlen;
}
```

The above method exceeded time limit. 

## Another way

```c
int lengthOfLongestSubstring(char* s) {
   int i =0, j = 0 ;
   int alphabets[128];
   int maxlen = 0, startLocation = -1, currentlen=0;
   
   memset(alphabets, -1, sizeof(alphabets));
   
   for ( i = 0 ; i < strlen(s) ; i++) {

       if (alphabets[s[i]] != -1) {
            // this part is important to keep startLocation in substring.
            startLocation = (alphabets[s[i]] > startLocation) ? alphabets[s[i]] : startLocation; 
            
       }
       alphabets[s[i]] = i;
       currentlen = i-startLocation;
       maxlen = ( maxlen > currentlen ) ? maxlen : currentlen; 
   }
   return maxlen;
}
```
if you wato plus 0ne to [i,j), the result is [i+1, j+1). 

basic concept is the same from right above, but it shrink count of for statement. 

**this sliding method is useful in array and string.**

# [Reference site : cplusplus](http://www.cplusplus.com/reference/clibrary/) 

[i,j) = {x | i <= x < j} is left-closed and right-open.

you need to konw about str functions.
  
> [memset](http://www.cplusplus.com/reference/cstring/memset/) : 
 
  - void * memset (void * ptr, int value, size_t num); 
  
  - Fill block of memory. **be careful that value is just type conversion from int to unsigned char.**
  
  - return ptr value. 
  
> [strlen](http://www.cplusplus.com/reference/cstring/strlen/) 

  - size_t strlen (const char *str);
  
  - return length of string except for NULL Charater in a string.
