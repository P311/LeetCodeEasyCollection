# LeetCodeEasyCollection
## [First Unique Character in a String](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/881/)
```python
from collections import Counter
class Solution:
    def firstUniqChar(self, s: str) -> int:  
        dic = {}
        for i in s:
            dic[i] = dic.get(i, 0) + 1
        for i in range(len(s)):
            if dic[s[i]] == 1:
                return i
        return -1
```
## [Valid Anagram](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/882/)
```python
from collections import Counter
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```
## [String to Integer (atoi)](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/884/)
```python
class Solution:
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        # Read in and ignore any leading whitespace.
        str = str.strip()
        # Check if the next character (if not already at the end of the string) is '-' or '+'. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.
        pos = True
        read_symbol = False
        num = ''
        for i in str:
            if i == '-' or i == '+':
                if not read_symbol:
                    pos = (i != '-')
                    read_symbol =True
                elif read_symbol:
                    break
            # Read in next the characters until the next non-digit charcter or the end of the input is reached. The rest of the string is ignored.
            elif i.isdigit():
                num += i
                read_symbol = True
            else:
                break
        # Convert these digits into an integer (i.e. "123" -> 123, "0032" -> 32). If no digits were read, then the integer is 0. Change the sign as necessary (from step 2).
        # Return the integer as the final result.
        if num == '':
            return 0
        else:
            # If the integer is out of the 32-bit signed integer range [-231, 231 - 1], then clamp the integer so that it remains in the range. Specifically, integers less than -231 should be clamped to -231, and integers greater than 231 - 1 should be clamped to 231 - 1.
            val = int(num) * -1 if not pos else int(num)
            return min(2**31-1, max(-2**31, val))
```
