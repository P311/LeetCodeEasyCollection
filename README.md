# LeetCodeCollection
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
## [Implement strStr()](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/885/)
``` python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if needle == '':
            return 0
        if haystack == "":
            return -1

        l, k = len(haystack), len(needle)
        for i in range(l):
            if haystack[i: i+k] == needle:
                return i
            i += 1
        return -1
```
###  [Longest Common Prefix](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/887/)
```python
        i = 0
        r = ''
        while True:
            cur = ''
            for s in strs:
                if i < len(s):
                    if cur == '':
                        cur = s[i]
                    elif s[i] != cur:
                        return r
                else:
                    return r
            r += cur
            i += 1
```

### [Longest Common Prefix](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/887/)
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        # ans = strs[0]
        # if len(strs) == 0:
        #     return ''
        # n = min([len(s) for s in strs])
        # if len(strs) == 1:
        #     return ans
        # for i in range(1, len(strs)):
        #     tmp = ''
        #     print(ans, strs[i], i)
        #     for j in range(min(len(ans), n)):
        #         if ans[j] != strs[i][j]:
        #             break
        #         else:
        #             tmp += strs[i][j]
        #     ans = tmp
        # return ans

    
        i = 0
        l = min([len(s) for s in strs])
        r = ''
        a = strs[0]
        while i < l:
            if all([s[i] == a[i] for s in strs]):
                r += a[i]
                i += 1
            else:
                return r
        return r
            
```

### [Coin Change](https://leetcode.com/problems/coin-change/)
```
class Solution:
    def coinChange(self, coins: List[int], amount: int, dic = {}) -> int:
        if amount == 0:
            return 0
        q = []
        for i in coins:
            q.append((i, 1))
        s = set()
        while q != []:
            cur = q.pop(0)
            for coin in coins:
                if cur[0] == amount:
                    return cur[1]
                elif cur[0] + coin > amount:
                    continue
                elif cur[0] + coin not in s:
                    s.add(cur[0] + coin)
                    q.append((cur[0] + coin, cur[1] + 1))
        return -1
             
        
        # if amount == 0:
        #     return 0
        # arr = [math.inf for i in range(amount + 1)]
        # for coin in coins:
        #     if coin <= amount:
        #         arr[coin] = 1
        # for i, j in enumerate(arr):
        #     if j != -1:
        #         for coin in coins:
        #             if i + coin <= amount:
        #                 arr[i+coin] = min(arr[i+coin], arr[i] + 1)
        # if arr[-1] == math.inf:
        #     return -1
        # return arr[-1]
            
            
        # if amount == 0:
        #     return 0
        # if coins == []:
        #     return -1
        # cur = coins[0]
        # i = 0
        # mi = math.inf
        # while i * cur <= amount:
        #     val = self.coinChange(coins[1:], amount - i * cur)
        #     if val != -1:
        #         mi = min(i + val, mi)
        #     i += 1
        # if mi == math.inf:
        #     return -1
        # return mi
```

### [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)
```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        r = 0
        l1, l2 = len(text1), len(text2)
        s = [[0 for i in range(l2+1)] for j in range(l1+1)]
        for i in range(1, l1+1):
            for j in range(1, l2+1):
                if text1[i-1] == text2[j-1]:
                    s[i][j] = max(s[i-1][j], s[i][j-1], 1 + s[i-1][j-1])
                else:
                    s[i][j] = max(s[i-1][j], s[i][j-1])
        return s[-1][-1]
                   
```
