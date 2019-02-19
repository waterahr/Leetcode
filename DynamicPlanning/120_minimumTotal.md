# 120.三角形最小路径和

设dp[i][j]表示到达坐标(i, j)处的最小路径和,递推关系式为:dp[i][j]=min(dp[i-1][j], dp[i-1][j-1])+triangle[i][j].

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<vector<int>> dp(triangle);
        for(int i=1; i<triangle.size(); i++)
            for(int j=0; j<=i; j++){
                if(j==0)
                    dp[i][j] += dp[i-1][j];
                else if(j==i)
                    dp[i][j] += dp[i-1][j-1];
                else
                    dp[i][j] += min(dp[i-1][j], dp[i-1][j-1]);
            }
        int last_row = triangle.size() - 1, min_path = INT_MAX;
        for(int path:dp[last_row])
            min_path = min(min_path, path);
        return min_path;
    }
};
```
