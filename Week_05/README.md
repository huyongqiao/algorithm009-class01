#### 学习笔记
```python

```

#### 代码
```python
# 不同路径，62
# 最右边和最下变的为1，然后从右下角递推到左上角，ll[0][0]就是求解的值
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        ll = [[1 if j == m - 1 or i == n - 1 else 0 for j in range(m)] for i in range(n)]
        for i in range(n - 2, -1, -1):
            for j in range(m - 2, -1, -1):
                ll[i][j] = ll[i][j + 1] + ll[i + 1][j]
        return ll[0][0]


# 不同路径，63
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m, n = len(obstacleGrid[0]), len(obstacleGrid)
        # 如果右下角为障碍物，不用计算了，直接返回0，否则右下角为1，右侧和下侧包一层0开始计算
        if obstacleGrid[n - 1][m - 1] == 1:
            return 0
        ll = [[0 for j in range(m + 1)] for i in range(n + 1)]
        for i in range(n - 1, -1, -1):
            for j in range(m - 1, -1, -1):
                if i == n - 1 and j == m - 1:
                    ll[i][j] = 1
                else:
                    ll[i][j] = ll[i][j + 1] + ll[i + 1][j] if obstacleGrid[i][j] == 0 else 0
        return ll[0][0]

# 最长公共子序列 1143
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        if not text1 or not text2:
            return 0
        m, n = len(text1), len(text2)
        dp = [[0] * (n + 1) for _ in range(m + 1)]
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if text1[i - 1] == text2[j - 1]:
                    dp[i][j] = 1 + dp[i - 1][j - 1]
                else:
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
        return dp[m][n]


# 三角形最小路径之和，120
# 一维DP，没有保存中间结果
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        if not triangle:
            return 0
        dp = triangle[-1]
        n = len(triangle)
        for i in range(n - 2, -1, -1):
            for j in range(len(triangle[i])):
                dp[j] = min(dp[j], dp[j+1]) + triangle[i][j]
        return dp[0]

# 最大子序列，53
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        import copy
        dp = copy.copy(nums)
        for i in range(1, len(dp)):
            dp[i] = max(nums[i], nums[i] + dp[i - 1])
        return max(dp)

# 零钱兑换，322
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [-1] * (amount + 1)
        dp[0] = 0
        for i in range(1, amount + 1):
            nums = []
            for coin in coins:
                if i >= coin and dp[i-coin] != -1:
                    nums.append(dp[i-coin])
            if nums:
                dp[i] = min(nums) + 1
        return dp[amount]

# 打家劫舍，108
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        n = len(nums)
        dp = [[0, 0] for _ in range(n)]
        # 二维的0表示不偷，1表示偷
        dp[0][0] = 0
        dp[0][1] = nums[0]
        for i in range(1, n):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1])
            dp[i][1] = dp[i-1][0] + nums[i]
        return max(dp[n-1][0], dp[n-1][1])
        
```