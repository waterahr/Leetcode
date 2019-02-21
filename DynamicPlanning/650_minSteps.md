# 650.只有两个字的键盘

dp[i]表示在屏幕上打印i个字符的最少操作步骤,递推关系式为:dp[i]=min{i, dp[j]+i/j-1(已经打印了j个在屏幕上)+1(复制操作)}(1<=j<=i//2, i%j==0).

```cpp
class Solution {
public:
    int minSteps(int n) {
        vector<int> dp(n+1, 0);
        for(int i=2; i<=n; i++){
            dp[i] = i;
            for(int j=1; j<=i/2; j++){
                if(i%j == 0)
                    dp[i] = min(dp[i], dp[j]+i/j);
            }
        }
        return dp[n];
    }
};
```
