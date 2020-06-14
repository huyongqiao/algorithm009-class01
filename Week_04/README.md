#### 学习笔记
```python
# 深度优先遍历模板
visited = set()
def dfs(root, visited):
    if root in visited:
        return
    visited.add(root)
    for node in root.children:
        if node not in visited:
            self.dfs(node, visited)

# 广度优先遍历模板
def bfs(root):
    from collections import deque
    queue = deque([root])
    while queue:
        node = queue.popleft()
        for child in node.children:
            queue.append(child)

# 二分查找模板
left, right = 0, len(array) - 1
while left <= right:
    mid = (left + right) // 2
    if array[mid] == target:
        return mid
    elif array[mid] < target:
        left = mid + 1
    else:
        right = mid - 1
```

#### 作业
```python
# 二叉树层次遍历，bfs实现
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []
        from collections import deque
        queue = deque([root])
        res = []
        while queue:
            level_data = []
            level_length = len(queue)
            for _ in range(level_length):
                node = queue.popleft()
                level_data.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            res.append(level_data)
        return res

# 二叉树层次遍历，dfs实现
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []

        res = []
        def dfs(level, node, res):
            if not node:
                return
            if len(res) < level + 1:
                res.append([])
            level_data = res[level] 
            level_data.append(node.val)
            dfs(level + 1, node.left, res)
            dfs(level + 1, node.right, res)
        dfs(0, root, res)
        return res

# 岛屿数量，使用dfs实现
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid:
            return 0
        x_length, y_length = len(grid), len(grid[0])
        res = 0

        def dfs(x, y):
            if x in (-1, x_length) or y in (-1, y_length) or grid[x][y] == '0':
                return
            grid[x][y] = '0'
            dfs(x + 1, y)
            dfs(x - 1, y)
            dfs(x, y + 1)
            dfs(x, y - 1)

        for x in range(x_length):
            for y in range(y_length):
                if grid[x][y] == '1':
                    res += 1
                    dfs(x, y)
        return res

# 饼干分发
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        if not g or not s:
            return 0
        res = 0
        g.sort(reverse=True)
        s.sort(reverse=True)
        while g and s:
            if s.pop() >= g[-1]:
                res += 1
                g.pop()
        return res

# 买卖股票的最佳时机
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        for i in range(1, len(prices)):
            if prices[i] > prices[i-1]:
                res += prices[i] - prices[i - 1]
        return res

# 跳跃游戏
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        if not nums:
            return False
        end = len(nums) - 1
        for i in range(end, -1, -1):
            if nums[i] + i >= end:
                end = i
        return end == 0

# x的平方根
class Solution:
    def mySqrt(self, x: int) -> int:
        if x <= 1:
            return x
        left, right = 0, x
        while left <= right:
            mid = (left + right) // 2
            tmp = mid * mid
            if tmp == x:
                return mid
            elif tmp < x:
                left = mid + 1
                res = mid
            else:
                right = mid - 1
        return res
```