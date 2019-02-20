# 279.完全平方数

dp[n]表示当前情况下和等于n所需的完全平方数的最小个数(之所以说当前情况下是因为动态规划只考虑之前见过的情况而不考虑之后的情况),递推关系式为:
dp[n]=min{1+dp[n-i*i]}(1<=i*i<=n).

```cpp
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n+1, 0);
        dp[1] = 1;
        for(int i=2; i<=n; i++){
            dp[i] = i;
            for(int j=1; j*j<=i; j++)
                dp[i] = min(dp[i], dp[i-j*j]+1);
        }
        return dp[n];
    }
};
```
