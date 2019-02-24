# 375.猜数字大小II

dp[i][j]表示从[i,j]中猜出正确数字所需要的最少花费金额(dp[i][i] = 0).假设在范围[i,j]中选择x, 则选择x的最少花费金额为: 
dp[i][j]=max(dp[i][x-1], dp[x+1][j])+x.

```cpp
class Solution {
public:
    int getMoneyAmount(int n) {
        vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));
        for (int j=2; j<=n; j++){
            for (int i=j-1; i>0; i--){
                int global_min = INT_MAX;
                for (int k=i+1; k<j; k++){
                    int local_max = k + max(dp[i][k - 1], dp[k + 1][j]);
                    global_min = min(global_min, local_max);
                }
                dp[i][j] = i + 1 == j ? i : global_min;
            }
        }
        return dp[1][n];
    }
};
```
