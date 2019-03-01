# 85.最大矩形

dp_h[i][j]表示在grid[i, :]中以grid[i][j]为最末的单行矩形的最大面积,dp_v[i][j]表示在grid[:, j]中以grid[i][j]为最末的单列矩形的最大面积,
状态转移方程为:dp[i][j]==1?dp_h[i][j]=dp_h[i][j-1]+1;dp_v[i][j]=dp_v[i-1][j]+1.

```cpp
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        int m = matrix.size();
        if(m == 0) return 0;
        int n = matrix[0].size();
        if(n == 0) return 0;
        vector<vector<int>> dp_h(m+1, vector<int>(n+1, 0)), dp_v(dp_h), dp(dp_h);
        int max_area = 0;
        for(int i=1; i<=m; i++)
            for(int j=1; j<=n; j++)
                if(matrix[i-1][j-1] == '1'){
                    dp_h[i][j] = dp_h[i][j-1] + 1;
                    dp_v[i][j] = dp_v[i-1][j] + 1;
                    dp[i][j] = max(dp_h[i][j], dp_v[i][j]);
                    int height = 0, width = INT_MAX;
                    for(int k=i; k>=0; k--){
                        if(dp_h[k][j] == 0) break;
                        height++;
                        width = min(width, dp_h[k][j]);
                        dp[i][j] = max(dp[i][j], height * width);
                    }
                    max_area = max(max_area, dp[i][j]);
                }
        return max_area;
    }
};
```
