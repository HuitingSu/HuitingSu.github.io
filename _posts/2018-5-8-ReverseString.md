---
layout: post
title: Reverse String and Words in String
---

### Reverse String
Write a function that takes a string as input and returns the string reversed.    
Example:   
Given s = "hello", return "olleh".

Use the slow and fast pointer to do in-place reverse.

Solution:
```Javascript
class Solution {
    public String reverseString(String s) {
        int i = 0; 
        int j = s.length() - 1;
        char[] c = s.toCharArray();  // need to convert to char array
        char tmp;
        while(i < j){
            tmp = c[i];
            c[i] = c[j];
            c[j] = tmp;
            i++;
            j--;
        }
        return new String(c);       // convert back to string 
    }
}
```

### Reverse Words in a String
Given an input string, reverse the string word by word.  
Note:
*A word is defined as a sequence of non-space characters.
*Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
*You need to reduce multiple spaces between two words to a single space in the reversed string.

This is combined by two basic problems:
1. Reverse a string using two pointer moving from head and tail to the middle
2. Use slow and fast pointer to eliminate extra spaces in a in-place way

It can be solved in 2 steps:
1. Reverse the entire string
2. Eliminate spaces, and after reading one word, reverse that word.

```python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        # because string in python is immutable, convert it as a list
        s = list(s)
        slow = 0
        fast = 0
        self.reverseArray(s, 0, len(s)-1)
        s.append(' ')       # add a space to the end of the array for convenience
    
        is_char = False
        while(fast < len(s)):
            # the first char I find
            if(s[fast] != ' ' and is_char == False):  
                if(slow > 0):
                    s[slow] = ' '
                    slow += 1
                is_char = True
                s[slow] = s[fast]
                word_head = slow
                slow += 1
            
            # inside a word. It is crucial to use 'elif' instead of if 
            # because the previous if change the value of several variables
            elif(s[fast] != ' ' and is_char == True):  
                s[slow] = s[fast]
                slow += 1                
                
            # detect word end, then reverse the word
            elif(s[fast] == ' ' and is_char == True):  
                self.reverseArray(s, word_head, slow-1)
                is_char = False
            fast += 1
           
        return ''.join(s[0:slow])            # convert the array back to string
         
    def reverseArray(self, array, i, j):
        while(i < j):
            tmp = array[i]
            array[i] = array[j]
            array[j] = tmp
            i += 1
            j -= 1
```
