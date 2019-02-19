# 343.整数拆分

dp[n]表示将正整数拆分可以获得的最大乘积,考虑拆分成两个数的和,利用分治+动态规划的思想,递推关系式为:dp[n]=max{max(dp[i]*(n-i), i*(n-i))}(1<=i<=n-1).
PS:需要特别注意的就是，不要遗漏了i*(n-i)这种特殊情况，例如3.

```cpp
class Solution {
public:
    int integerBreak(int n) {
        vector<int> dp(n+1, 0);
        dp[1] = dp[2] = 1;
        for(int i=3; i<=n ;i++)
            for(int j=1; j<i; j++)
                dp[i] = max(dp[i], max(j*(i-j), dp[j]*(i-j)));
        return dp[n];
        
    }
};
```
