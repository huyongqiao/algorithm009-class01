#### 笔记
```python
# 二叉搜索树，删除节点的时候，把当前节点的右子树的最小值替换过来就行了


# 二叉堆实现简单，但是性能不是最好的，性能最好的是严格的斐波那契堆，实现比较复杂
# 二叉大顶堆性质：1.完全二叉树；2.任意根节点的值都大于等于子节点的值

insert
1.先插入到堆的尾部；
2.调整在堆中的位置，HeapifyUp一层一层向上浮动，和父节点比较并交换位置，时间复杂度O(logn)；

delete max
1.将堆尾的元素替代到堆顶；
2.调整在堆中的位置，HeapifyDown一层一层向下浮动，和子节点比较并交换位置，时间复杂度O(logn)


python实现的heapq里默认的是小顶堆，注意没有最大堆，只能删除堆顶元素，不能删除其他位置的元素
# heap堆结构的底层实现是完全二叉树的一维列表，满足任意根节点的值都小于子节点的值
# heappush(heap, x)  先将x放入列表末尾，执行HeapifyUp操作，直接调整列表结构，没有返回值
# heappop(heap)  将堆顶元素弹出，把列表末尾元素放入堆顶，执行HeapifyDown操作，直接调整列表结构，返回弹出的堆顶元素
# heapreplace(heap, x)  将堆顶元素弹出，把新元素放入堆顶，执行HeapifyDown操作，直接调整列表结构，返回弹出的堆顶元素
# heapify(l)  直接将一维数据堆化
# nlargest(3, l)  取堆中最大的3个元素
# nsmallest(3, l)  取堆中最小的3个元素
>>> from heapq import heappush, heappop, heapify, heapreplace, nlargest, nsmallest
>>> heap = []
>>> heappush(heap, 9)
>>> heap
[9]
>>> heappush(heap, 8)
>>> heap
[8, 9]
>>> heappush(heap, 7)
>>> heap
[7, 9, 8]
>>> heappush(heap, 6)
>>> heap
[6, 7, 8, 9]
>>> heappush(heap, 5)
>>> heap
[5, 6, 8, 9, 7]
>>> heappop(heap)
5
>>> heap
[6, 7, 8, 9]
>>> heapreplace(heap, 10)
6
>>> heap
[7, 9, 8, 10]
>>> l = [10, 9, 8, 7]
>>> heapify(l)
>>> l
[7, 9, 8, 10]
>>> nlargest(3, l)
[10, 9, 8]
>>> nsmallest(3, l)
[7, 8, 9]
```

#### 有效的字母异位词
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        d1, d2 = {}, {}
        for c in s:
            d1[c] = d1.get(c, 0) + 1
        for c in t:
            d2[c] = d2.get(c, 0) + 1
        return d1 == d2
```

#### 两数之和
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        d = {}
        for i, v in enumerate(nums):
            if target - v in d:
                return [i, d[target - v]]
            else:
                # 字典key存储值，value存储值对应的索引
                d[v] = i
```

#### N叉树的前序遍历
```python
class Solution:
    def preorder(self, root: 'Node') -> List[int]:
        if not root:
            return []
        res = [root.val]
        for child in root.children:
             res += self.preorder(child)
        return res
```

#### 字母异位词分组
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        d = {}
        for s in strs:
            key = ''.join(sorted(s))
            if key not in d:
                d[key] = [s]
            else:
                d[key].append(s)
        return list(d.values())
```

#### 二叉树中序遍历
```python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)
```

#### 二叉树前序遍历
```python
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        return [root.val] + self.preorderTraversal(root.left) + self.preorderTraversal(root.right)
```

#### N叉树的层次遍历（429）
```python
class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        if not root:
            return []
        from collections import deque
        nodes, res = deque([root]), []
        while nodes:
            level = []
            for _ in range(len(nodes)):
                node = nodes.popleft()
                level.append(node.val)
                nodes.extend(node.children)
            res.append(level)
        return res
```

#### 丑数（49）
```python
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        dp, a, b, c = [1] * n, 0, 0, 0
        for i in range(1, n):
            n2, n3, n5 = dp[a] * 2, dp[b] * 3, dp[c] * 5
            dp[i] = min(n2, n3, n5)
            if dp[i] == n2: a += 1
            if dp[i] == n3: b += 1
            if dp[i] == n5: c += 1
        return dp[-1]
```

#### 前K个高频元素
```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        d = {}
        for num in nums:
            d[num] = d.get(num, 0) + 1
        heap = list(d.values())
        from heapq import heapify
        heapify(heap)
        counts = set(nlargest(k, heap))
        res = []
        for k, v in d.items():
            if v in counts:
                res.append(k)
        return res
```