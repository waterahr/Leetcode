# 64.最小路径和

dp[i][j]表示达到坐标(i, j)的位置的最小路径和,递推关系式为:dp[i][j]=min(dp[i-1][j]+cost[i][j], dp[i][j-1]+cost[i][j]).

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        vector<vector<int>> dp(m, vector<int>(n, INT_MAX));
        dp[0][0] = grid[0][0];
        for(int i=0; i<m; i++)
            for(int j=0; j<n; j++){
                if(i - 1 >= 0)
                    dp[i][j] = min(dp[i][j], dp[i-1][j] + grid[i][j]);
                if(j - 1 >= 0)
                    dp[i][j] = min(dp[i][j], dp[i][j-1] + grid[i][j]);
            }
        return dp[m-1][n-1];
    }
};
```
