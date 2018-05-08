---
layout: post
title: Problems Related to Reverse
---

## Reverse String
Write a function that takes a string as input and returns the string reversed.
Example:
Given s = "hello", return "olleh".

### Solution
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
