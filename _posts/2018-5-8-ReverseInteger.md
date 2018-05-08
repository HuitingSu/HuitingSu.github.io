---
layout: post
title: Reverse Integer
---

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
