# 63.不同路径II

dp[i][j]表示到达坐标(i, j)位置处的路径个数,状态转移方程为:
nums[i][j]!=1?dp[i][j]=dp[i-1][j]+dp[i][j-1]:0.

```cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        if(m == 0) return 0;
        int n = obstacleGrid[0].size();
        vector<vector<long>> dp(m+1, vector<long>(n+1, 0));
        dp[1][0] = 1 - obstacleGrid[0][0];
        for(int i=1; i<=m; i++)
            for(int j=1; j<=n; j++){
                if(obstacleGrid[i-1][j-1] == 1)
                    dp[i][j] = 0;
                else
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        return dp[m][n];
    }
};
```
