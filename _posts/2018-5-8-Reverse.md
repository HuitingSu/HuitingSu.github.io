---
layout: post
title: Problems Related to Reverse
---

### Reverse String
Write a function that takes a string as input and returns the string reversed.    
Example:   
Given s = "hello", return "olleh".

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

### Reverse Integer

Given a 32-bit signed integer, reverse digits of an integer. Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        signof = lambda x:(1,-1) [x<0]
        sign = signof(x)
        x = abs(x)
        result = 0
        while(x > 0):    
            tail = x % 10
            result = tail + result * 10
            if((sign > 0 and result > 2**31-1) or (sign <0 and result > 2**31)):
                return 0                              ## if overflow, the value will change 
            x = x / 10
        return sign * result
```

### Reverse Linked List
A linked list can be reversed either iteratively or recursively. Could you implement both?

##### Iteratively
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None:
            return head
        
        prev = None
        cur = head
        nt = head.next
        
        while cur:
            cur.next = prev
            prev = cur
            cur = nt
            if nt:
                nt = nt.next
        return prev
```

##### Recursively
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None:
            return head
        if head.next == None:
            new_head = head
        else:
            new_head = self.reverseList(head.next)
            head.next.next = head
            head.next = None
        return new_head
```

### Reverse Words in a String
Given an input string, reverse the string word by word.  
Note:
*A word is defined as a sequence of non-space characters.
*Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
*You need to reduce multiple spaces between two words to a single space in the reversed string.

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
