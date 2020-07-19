#### 学习笔记
```python

```

#### 代码
```python
# 387 字符串中的第一个唯一字符
class Solution:
    def firstUniqChar(self, s: str) -> int:
        from collections import OrderedDict
        d = OrderedDict()
        for c in s:
            d[c] = d.get(c, 0) + 1
        for k, v in d.items():
            if v == 1:
                return s.index(k)
        return -1

 # 14. 最长公共前缀
 class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs:
            return ''
        length = min([len(str) for str in strs])
        public_str = ''
        for i in range(length):
            s = {str[i] for str in strs}
            if len(s) == 1:
                public_str += s.pop()
            else:
                break
        return public_str
                
               
 # 344. 反转字符串
 class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        length = len(s)
        for i in range(length // 2):
            s[i], s[-i-1] = s[-i-1], s[i]
        return s

# 151. 翻转字符串里的单词
 class Solution:
    def reverseWords(self, s: str) -> str:
        s = s.strip()
        words = s.split(' ')      
        return ' '.join(filter(lambda e: True if e else False, reversed(words)))

```