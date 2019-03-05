# 174.地下城游戏

倒着寻找状态转移方程,dp[i][j]表示到达grid[i-1][j-1]需要的最小的生命值,状态转移方程为:
```
dp[i][j]=max(1, min(dp[i+1][j], dp[i][j+1])-grid[i-1][j-1]).
```

```cpp
class Solution {
public:
    int calculateMinimumHP(vector<vector<int>>& dungeon) {
        int m = dungeon.size();
        int n = dungeon[0].size();
        
        vector<vector<int>> dp(m+1, vector<int>(n+1, INT_MAX));
        dp[m][n-1] = dp[m-1][n-1] = 1;
        for(int i=m-1; i>=0; i--)
            for (int j=n-1; j>=0; j--)
                dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j]);
        return dp[0][0];
    }
};
```
