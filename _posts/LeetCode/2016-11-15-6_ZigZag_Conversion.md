---
layout: post
title: 6. ZigZag Conversion (Difficulty-Easy)
subtitle: Difficulty - Easy
category: LeetCode
tags: [algorithm, c function, easy]
permalink: /2016/11/15/6_ZigZag_Conversion/
bigimg: 
    - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

# [6. ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/) 

The String "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this:(you may want to display this pattern in a fixed font for better legibility)

For Example

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line : "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows :

```
string convert(string text, int nRows);
```

Convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

```c
char* convert(char* s, int numRows) {
    
}
```

# My Solution. 

```
nROWs = 3; 
P   A   H   N  | 1   5   9     13 | 4 4 4    
A P L S I I G  | 2 4 6 8 10 12 14 | 2 2 2 2 2 2
Y   I   R      | 3   7   11       | 4 4
```
```
nROWs = 4;
P     I     N  | 1     7       13 | 6 6
A   L S   I G  | 2   6 8    12 14 | 4 2 4 2   
Y A   H R      | 3 5   9  11      | 2 4 2
P     I        | 4     10         | 6
```
```
nROWs = 5;
P      H       | 1       9        | 8
A    S I       | 2     8 10       | 6 2
Y  I   R       | 3   7   11       | 4 4
P L    I  G    | 4 6     12 14    | 2 6 2
A      N       | 5       13       | 8
```

 I think as you can see the above situation, they have rule line by line.

 I will use this rule, I can make equation of the above rule. 
 
 
```c
char* convert(char* s, int numRows) {
    int lenOfS = strlen(s);
    char* returnString = (char *)malloc((size_t)(lenOfS+1));
    int i=0,j=0;
    int idx=0;
    int first=0, second=0;
    int flag=first;
    
    if (numRows == 1 || numRows == 0)
        return s;
    
    memset(returnString, 0, (size_t)(lenOfS+1));
    
    for (i=0 ; i < numRows ; i++) {
        j = i; // row
        
        first = numRows*2 - 2 - 2*i;
        second = 2*i;
        flag =0;
        
        while (j < lenOfS) {  
            returnString[idx++]=s[j]; // making string. 
            //printf("i : %d, j:%d, first : %d second : %d\n",i, j, first, second);
            if (i == 0)
                j += first;
            else if ( i == numRows-1)
                j += second;
            else if (flag == 0) {
                j += first;
                flag=1;
            }
            else {
                j += second;
                flag=0;
            }  
       }
    }
    
  return returnString;  
}
```


