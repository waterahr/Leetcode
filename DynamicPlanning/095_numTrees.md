# 96.不同的二叉搜索树

dp[i][j]表示区间[i, j]为节点的二叉搜索树的个数,递推关系式为:dp[i][j]=Sigma{dp[i][k-1]*dp[k+1][j]}(i<=k<=j).

```cpp
class Solution {
public:
    int numTrees(int n) {
        vector<vector<int>> dp(n, vector<int>(n, 1));
        vector<int> dict(n, 0);
        for(int i=n-1; i>=0; i--)
            for(int j=i+1; j<n; j++){
                dp[i][j] = dict[j-i];
                if(dp[i][j])
                    continue;
                for(int k=i; k<=j; k++){
                    int left = 1, right = 1;
                    if(k-1>=0) left = dp[i][k-1];
                    if(k+1<n) right = dp[k+1][j];
                    dp[i][j] += left * right;
                }
                dict[j-i] = dp[i][j];
            }
        return dp[0][n-1];
    }
};
```
