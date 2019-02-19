# 931.下降路径最小和

dp[i][j]表示下降路径的终点为坐标(i, j)时的最小和,递推关系式为:dp[i][j]=min(dp[i-1][k], dp[i-1][k-1], dp[i-1][k+1])+grid[i][j].

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& A) {
        int n = A.size();
        vector<vector<int>> dp(n, vector<int>(n, INT_MAX));
        int min_path = INT_MAX;
        for(int i=0; i<n; i++){
            dp[0][i] = A[0][i];
            if(n==1) min_path = min(min_path, dp[0][i]);
        }   
        for(int i=1; i<n; i++)
            for(int j=0; j<n; j++){
                dp[i][j] = min(dp[i][j], dp[i-1][j]);
                if(j>0) dp[i][j] = min(dp[i][j], dp[i-1][j-1]);
                if(j<n-1) dp[i][j] = min(dp[i][j], dp[i-1][j+1]) ;
                dp[i][j] += A[i][j];
                if(i == n-1) min_path = min(min_path, dp[i][j]);
            }
        return min_path;
    }
};
```
