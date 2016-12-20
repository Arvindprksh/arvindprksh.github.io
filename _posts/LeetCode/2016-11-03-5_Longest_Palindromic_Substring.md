---
layout: post
title: 5. Longest Palindromic Substring (Difficulty-Medium)
category: LeetCode
subtitle: Diffculty - Medium
tags: [algorithm, c function, medium]
permalink: /2016/11/03/5_Longest_Palindromic_Substring/
bigimg:  
    - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

# [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string S, find the longest palindomic substring in S. You may assume that the maximum lenght of S is 1000, and there exisits one unique longest plindromic substring. 

```c
char* longestPalindrome(char* s) {
    
}
```

# My Solution 

## Brute force : deal with the whole cases

 I think just simply after I make every case of substring. I check if that substring is palindromic.
 
 - First of all, I have to make all substrings. 
 
 - Second of all, and then I need to check if reversing the substring is the same as the original substring. 

```c
char* longestPalindrome(char* s) {
   int lenOfS = strlen(s);
   char * tempSubstring = (char *)malloc((size_t)(lenOfS+1));
   char * reverseSubstring = (char *)malloc((size_t)(lenOfS+1));
   char * returnStr=(char *)malloc((size_t)(lenOfS+1));
   char * copyOfs = s;
   int maxOfLen = -1; 
   int i = 0, j = 0, k = 0;
   
   // all indices
   for ( i = 0 ; i < lenOfS ; i++) {
     
        // all length
        for ( j = 0 ; j < lenOfS ; j++) {
           
           if (j+i+1 > lenOfS)
              break;
           
           // for normal substring 
           memset(tempSubstring, 0, (size_t)(lenOfS+1));
           strncpy(tempSubstring, copyOfs+i , (size_t)(j+1));
           //printf("tempSubstring : %s\n", tempSubstring);
           //printf("i : %d j : %d, len : %d\n", i, j, j+1);
           
           // for reversed substring
           memset(reverseSubstring, 0, (size_t)(lenOfS+1));
           for ( k = 0 ; k < j+1 ; k++) {
              reverseSubstring[k] = tempSubstring[j-k];
           }
           //printf("reverseSubstring : %s\n", reverseSubstring);
           
          if (strncmp(tempSubstring, reverseSubstring,strlen(tempSubstring)) == 0) {
              
              int temp=strlen(tempSubstring);
              
              if( maxOfLen < temp ) {
                    maxOfLen =  temp;         
                    memset(returnStr, 0 , (size_t)(lenOfS+1));
                    strncpy(returnStr, tempSubstring,(size_t)(temp));
              }    
          }
          //printf("returnStr : %s\n", returnStr);
        }
   }
   return returnStr;
}
```
    
 in the above case, for statement is three times.

## Another way to improve over the above method 1. 

 -first I have to avoid unnecessary re-computation in the above algorithm. 

 -BUT, it is useless to do like this. i.e adding if statement in the middle of the above second for statement is useless.
 
 -like the above, Time Limit Exceeded. 
 
 
```c
char* longestPalindrome(char* s) {
   int lenOfS = strlen(s);
  .........
   
   // all indices
   for ( i = 0 ; i < lenOfS ; i++) {
        // all length
        for ( j = 0 ; j < lenOfS ; j++) {
           
           if (j+i+1 > lenOfS)
              break;
              
           // if you know the current maxOfLen, you don't have to compute the case less than max 
           //printf("j+1 : %d, max : %d\n", j+1, maxOfLen);
           if (j + 1 < maxOfLen)
               continue;  
           
           ......    
          }
          //printf("returnStr : %s\n", returnStr);
        }
   }
   return returnStr;
}
```

## Anothe way to improve the time complexity of the above 2, From now on I will explain the easy way.

 - at first, reverse the whole string. 
 
 - after that, checking if the substring fits to reverse substrings
 
```c
char* longestPalindrome(char* s) {
    int lenOfS = strlen(s);
    char * reverseString = (char *)malloc((size_t)(lenOfS)+1);
    char * returnString = (char *)malloc((size_t)(lenOfS)+1);
    int maxLen=-1;
    int i = 0, j = 0; 
    
    memset(reverseString, 0, (size_t)(lenOfS+1));
    memset(returnString, 0, (size_t)(lenOfS+1));
    // make the reverse string. 
    for(i = 0 ; i < lenOfS ; i++){
        reverseString[i]=s[lenOfS-i-1];
    }
    //for check 
    //printf("s : %s\n", s);
    //printf("reverseString : %s\n", reverseString);
    
    
    for(i = 0 ; i < lenOfS ; i++) {
        
        for(j = 0 ; j + i  < lenOfS ; j++) {
            if (strncmp(&s[i], &reverseString[lenOfS-i-j-1], j+1 ) == 0) {
                if (maxLen < j+1) {
                    maxLen = j+1;
                    memset(returnString, 0, (size_t)(lenOfS+1));
                    strncpy(returnString, &reverseString[lenOfS-i-j-1], j+1);
                    //printf("returnString : %s, maxLen : %d\n",returnString, maxLen);
                }
            }
        }
    }
    return returnString;
}
```

   this choice is time limit exceeded. 

## Another way to improve over the above method 2

 - while searching for the total cases, if time limit exceed. 
 
 - Mostly, you have to use dynamic programming whithin searching problem. 
 
 - dynamic programming is divided into two way, recursive function or for statement 
 
 - If you use the following method, you can decrease useless operations. 
 
 - In this problem, feature of palindorme. 
 
```
    char * S = string.

           |----- true,       if the substring S[i]~S[j] is a palindrome.
    P(i,j) |
           |----- false,      otherwise.
           
    Therefore
            
                  P(i, j) = ( P(i-1, i-j) and S[i]==S[j] )
                  
    The base cases are :
    
                  P(i, i) = true and P(i, i+1) = (S[i]==s[i+1])
```

   - If you find recurivse equation, you can use the dynamic programming.
    
   - next stage, you can choose the method like how to make function between only using for statement and recursive function. 
    
   - the below is the case of only using for statement. 
    
   - when using dynamic programming, you typically need to use state array(dp array). 
    
   - it is similiar to BFS, DFS, Backtracking and so on.
    
   - in avobe case, similarity is with state array. 


```c  
// I use dp array 
// <-a->,  <-aa-> 
char* longestPalindrome(char* s) {
    char visited[1000][1000] = {0};
    int lenOfS = strlen(s);
    int maxLenOfSubstring=0;
    int i = 0, j = 0; 
    int startIdx = 0 , endIdx = 0;
    char * returnString = (char *)malloc((size_t)(lenOfS)+1);
    
    if (lenOfS == 1 || s == NULL)  
        return s;
    // length of substring is 1
    for (i = 0 ; i < lenOfS ; i++) {
        visited[i][i] = 1;
        maxLenOfSubstring = 1; 
    }
    
    // lenghth of 2
    for (i = 0 ; i < lenOfS-1 ; i++) {
        
        if (s[i] == s[i+1]) {
            //printf("if (s[%d] == s[%d])\n", i, i+1);
            visited[i][i+1] = 1;
            maxLenOfSubstring = 2;
            startIdx=i;
            endIdx=i+1;
        }
    }
    
    // above 3 elements;
    for ( i = 3 ; i <= lenOfS ; i++) {
        
           for (j = 0 ; j < (lenOfS - i + 1) ; j++) {
            
                int k = j + i -1;
            
                visited[j][k] = ((visited[j+1][k-1] == 1) && (s[j]==s[k]));
                
                if (visited[j][k] == 1){
                    maxLenOfSubstring = i;
                    startIdx=j;
                    endIdx=k;
                }
           }
    }
    memset(returnString, 0, (size_t)(lenOfS+1));
    return strncpy(returnString, &s[startIdx], maxLenOfSubstring);
}  
```   

---

## Another way to improver over the above method 3

  - just Expand around Center 
  
  - it is divided into two cases. one is length of center is 1, the other case is length of that is 2. 
  
  - for example, in 'aba', the center is 'b'.
  
  - another example of "abba", the center is between 'bb'. 
  
  - big hint : f(i-1, j-1) = true and s[i] == s[j] ----> f(i,j) is palindrome
  
  - with above equation, You just divid case into two, whether center is one element or two element.
  
 
```c 
static int ExpandAroundCenter(char * s, int left, int right) {

    while (left >=0 && right < strlen(s) && (s[left] == s[right])) {
        right=right+1;
        left=left-1;       
    }
    
    return right - left - 1; // the total length.  
}

char* longestPalindrome(char* s) {
    int lenOfS=strlen(s);
    int startIdx=0, endIdx=0;
    int maxOfLen = endIdx - startIdx;
    char * returnString = (char *)malloc((size_t)(lenOfS+1));
    int i=0, j=0; 
    
    for (i = 0; i < lenOfS ; i++) {
        int lenOfSubString1 = ExpandAroundCenter(s, i, i); 
        int lenOfSubString2 = ExpandAroundCenter(s, i, i+1);
        int maxLenOfSubStrings = (lenOfSubString1 > lenOfSubString2) ? lenOfSubString1 : lenOfSubString2;
        
          //  printf("i: %d -- lenOfSubString1: %d, lenOfSubString2: %d --maxLenOfSubStrings :%d\n",i, lenOfSubString1, lenOfSubString2,maxLenOfSubStrings);
        
        if (maxOfLen <= maxLenOfSubStrings) {
                startIdx = i - (maxLenOfSubStrings-1)/2;
                endIdx = i + maxLenOfSubStrings / 2;        
                maxOfLen=maxLenOfSubStrings;
        }
        
    }
    memset(returnString,0, strlen(s)+1);
   // printf("len : %d\n",endIdx - startIdx + 1 );
   // printf("startIdx:%d, endIdx:%d", startIdx, endIdx);
    return strncpy(returnString, &s[startIdx], endIdx - startIdx + 1); 
}
```
  
## Another algorithm 

# [Reference site : cplusplus](http://www.cplusplus.com/reference/clibrary/)

> [strncpy](http://www.cplusplus.com/reference/cstring/strncpy/)  
  
  - char * strncpy ( char * destination, const char * source, size_t num);
  
  - This function always deal with NULL value, So you have to be careful of this point.
  
  
> [strncmp](http://www.cplusplus.com/reference/cstring/strncmp/)

  - int strncmp ( const char * str1, const char * str2, size_t num);
  
  - size_t is an unsigned integral type
