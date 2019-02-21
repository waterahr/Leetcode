# 264.丑数II

所有的丑数都是由已有的丑数乘上2,3,5得到的,故设置三个指针依次乘即可.

```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        int idx_two = 0, idx_three = 0, idx_five = 0;
        vector<int> dp(n, 1);
        for(int i=1; i<n; i++){
            dp[i] = min(dp[idx_two]*2, min(dp[idx_three]*3, dp[idx_five]*5));
            if(dp[i] == dp[idx_two]*2) idx_two++;
            else if(dp[i] == dp[idx_three]*3) idx_three++;
            else idx_five++;
        }
        return dp.back();
    }
};
```
