#### 学习笔记
```python
AVL: 严格平衡二叉搜索树，旋转频次高，从读的角度来说，AVL更好，需要更多的内存来存额外的信息factor和height，适合读操作比较多的操作，在DB里用的相对多
红黑树：近似平衡二叉搜索树，降低旋转频次，从写的角度来说，红黑树更好，只需要1bit来存储红或者黑，适合写操作比较多的操作，在map/set里用的比较多

```


#### 作业
```python
# 字典树
# 需要注意的点：
# 1.字典的层级获取，d.setdefault(c, {})，相当于先get获取，有结果时返回，无结果时赋默认值并返回
# 2.结束字符的处理，区分叶子节点和中间节点
class Trie(object):
    def __init__(self):
        self.root = {}
        self.end = '#'
        
    def insert(self, word):
        d = self.root
        for c in word:
            # if char in d:
            #     d = d[char]
            # else:
            #     d[char] = {}
            #     d = d[char]
            d = d.setdefault(c, {})
        d[self.end] = self.end

    def search(self, word):
        d = self.root
        for c in (word + self.end):
            d = d.get(c)
            if d is None:
                return False
        return True
        
    def startsWith(self, prefix):
        d = self.root
        for c in prefix:
            d = d.get(c)
            if d is None:
                return False
        return True


# 并查集，岛屿问题
# 使用并查集
class UnionFind:
    def __init__(self, grid):
        m, n = len(grid), len(grid[0])
        self.parent = [-1] * (m * n)
        self.count = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1':
                    self.parent[i * n + j] = i * n + j
                    self.count += 1

    def find(self, val):
        while self.parent[val] != val:
            val = self.parent[val]
        return val

    def union(self, x, y):
        rootx = self.find(x)
        rooty = self.find(y)
        if rootx != rooty:
            self.parent[rooty] = rootx
            self.count -= 1
            
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid or not grid[0]:
            return 0

        uf = UnionFind(grid)
        m, n = len(grid), len(grid[0])
        dx = (-1, 1, 0, 0)
        dy = (0, 0, -1, 1)

        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1':
                    for k in range(4):
                        x, y = i + dx[k], j + dy[k]
                        if 0 <= x < m and 0 <= y < n and grid[x][y] == '1':
                            uf.union(i * n + j, x * n + y)
        return uf.count

# N皇后问题
class Solution:
    def totalNQueens(self, n: int) -> int:
        self.n = n
        self.res = []
        self.dfs([], [], [])
        return len(self.res)
    
    def dfs(self, queens, xy_dif, xy_sum):
        x = len(queens)
        if x == self.n:
            self.res.append(queens)
            return
        for y in range(self.n):
            if y not in queens and x - y not in xy_dif and x + y not in xy_sum:
                self.dfs(queens + [y], xy_dif + [x - y], xy_sum + [x + y])

```