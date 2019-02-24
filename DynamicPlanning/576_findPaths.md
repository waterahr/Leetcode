# 576.出界的路径数

dp[k][i][j]表示在坐标(i, j)处开始移动k步将棋子移动出界的不同的路径个数,状态转移方程为:
dp[k][i][j]=dp[k-1][i+1][j]+dp[k-1][i-1][j]+dp[k-1][i][j-1]+dp[k-1][i][j+1].

```cpp
class Solution {
public:
    int findPaths(int m, int n, int N, int i, int j) {
        vector<vector<vector<int>>> dp(N+1, vector<vector<int>>(m, vector<int>(n, 0)));
        vector<pair<int, int>> directions = {{-1,0},{1,0},{0,-1},{0,1}};
        for(int k=1; k<=N; k++)
            for(int i=0; i<m; i++)
                for(int j=0; j<n; j++)
                    for(auto dire:directions){
                        int next_i = i + dire.first, next_j = j + dire.second;
                        if(next_i >= 0 && next_i < m && next_j >= 0 && next_j < n)
                            dp[k][i][j] = (dp[k][i][j] + dp[k-1][next_i][next_j]) % 1000000007;
                        else
                            dp[k][i][j] += 1;
                    }
        return dp[N][i][j];
    }
};
```
