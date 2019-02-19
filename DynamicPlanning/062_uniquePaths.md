# 62.不同路径

设dp[i][j]表示到达坐标(i, j)位置的不同路径个数,递推关系式为:dp[i][j]=dp[i-1][j]+dp[i][j-1].

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        dp[0][1] = 1;
        for(int i=1; i<=m; i++)
            for(int j=1; j<=n; j++)
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
        return dp[m][n];
    }
};
```
