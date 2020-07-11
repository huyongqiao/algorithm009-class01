#### 学习笔记
```python
1.将x最右边的n位清零：x & (~0<<n)
2.获取x的第n位值：(x >> n) & 1
3.获取x的第n位的幂值：x & (1 << n)
4.仅将第n位置为1: x | (1 << n) 
5.仅将第n位置为0: x & (~(1 << n))
6.将x最高位至第n位（含）清零: x & ((1<<n)-1)

判断奇偶：
x & 1 == 1 
x & 1 == 0

除2
x >> 1

清零最低位的1：
x = x & (x - 1)

得到最低位的1： -x = ~x + 1
x & -x   
 
```

#### 代码
```python
# 1的个数，191
class Solution(object):
    def hammingWeight(self, n):
        # 解法1：逐位判断
        num = 0
        while n:
            if n & 1:
                num += 1
            n = n >> 1
        return num
    
        # 解法2：异或操作
        num = 0
        while n:
            num += 1
            n = n & (n - 1)
        return num

# 2的幂
class Solution(object):
    def isPowerOfTwo(self, n):
        return n > 0 and n & (n - 1) == 0

# 比特位计数
# 使用动态规划
# num中1的个数 = num去除最低位的1后1的个数 + 1
# num去除最低位的1后肯定比num小，所以先计算处理
class Solution:
    def countBits(self, num: int) -> List[int]:
        counts = [0] * (num + 1)
        for i in range(1, num + 1):
            counts[i] = counts[i & (i - 1)] + 1
        return counts


# Python 布隆过滤器实现
from bitarray import bitarray
import mmh3


class BloomFilter:

    def __init__(self, size, hash_num):
        self.size = size
        self.hash_num = hash_num
        self.bit_array = bitarray(size)
        self.bit_array.setall(0)

    def add(self, s):
        for seed in range(self.hash_num):
            index = mmh3.hash(s, seed) % self.size
            self.bit_array[index] = 1

    def exists(self, s):
        for seed in range(self.hash_num):
            index = mmh3.hash(s, seed) % self.size
            if self.bit_array[index] == 0:
                return False
        return True


bf = BloomFilter(1024, 10)
bf.add('hello')
print(bf.exists('hello'))
print(bf.exists('world'))


# LRU 
# 使用有序字典实现，时间复杂度为O(1)
import collections

class LRUCache:

    def __init__(self, capacity: int):
        self.d = collections.OrderedDict()
        self.remain = capacity

    def get(self, key: int) -> int:
        if key not in self.d:
            return -1
        res = self.d.pop(key)
        self.d[key] = res
        return res

    def put(self, key: int, value: int) -> None:
        if key in self.d:
            self.d.pop(key)
        else:
            if self.remain:
                self.remain -= 1
            else:
                self.d.popitem(last=False)
                # self.d.popitem(0)
        self.d[key] = value          

```