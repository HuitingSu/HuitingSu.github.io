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

Here's a line for us to start with.

This line is separated from the one above by two newlines, so it will be a *separate paragraph*.

This line is also a separate paragraph, but...
This line is only separated by a single newline, so it's a separate line in the *same paragraph*.
