# 357.计算各个位数不同的数字个数

dp[n]表示区间[0, 10^n)内的数字各个位数不同的数字个数.分析可知,递推关系式为:dp[n] = dp[n-1] + 9*9*8*...*(11-n).

```cpp
class Solution {
public:
    int countNumbersWithUniqueDigits(int n) {
        if(n == 0) return 1;
        vector<int> dp(n+1, 0);
        dp[1] = 10;
        for(int i=2; i<=n; i++){
            int add = 81;
            for(int j=1; j<=i-2; j++)
                add *= (9-j);
            dp[i] = dp[i-1] + add;
        }
        return dp[n];
    }
};
```
