
## [405. Convert a Number to Hexadecimal](https://leetcode.com/problems/convert-a-number-to-hexadecimal/description/)

Given an integer, write an algorithm to convert it to hexadecimal. For negative integer, two’s complement method is used.

Note:

All letters in hexadecimal (a-f) must be in lowercase.
The hexadecimal string must not contain extra leading 0s. If the number is zero, it is represented by a single zero character '0'; otherwise, the first character in the hexadecimal string will not be the zero character.
The given number is guaranteed to fit within the range of a 32-bit signed integer.
You must not use any method provided by the library which converts/formats the number to hex directly.
(把十进制数字转化为十六进制)

```
Example 1:

	Input: 26
	Output: "1a"

Example 2:

	Input: -1
	Output:"ffffffff"
```

###### 解题思路
```
class Solution(object):
    def toHex(self, num):
		 
        if num == 0: return '0'
        
        ans = ''
        s = '0123456789abcdef'
        # 负数 加2**32
        if num < 0:
            num += 2 ** 32
        
        while num > 15:
            ans = s[num % 16] + ans
            num = num / 16
        ans = s[num] + ans  
            
        return ans
```