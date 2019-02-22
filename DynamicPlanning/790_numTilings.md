# 790.多米诺和托米诺平铺

dp[i] = 2*dp[i-1] + dp[i-3]

```cpp
class Solution {
public:
    int numTilings(int N) {
        vector<int> dp(N, 0);
        dp[0] = 1;
        if(N == 1) return 1;
        dp[1] = 2;
        if(N == 2) return 2;
        dp[2] = 5;
        if(N == 3) return 5;
        
        for(int i=3; i<N; i++)
            dp[i] = ((2 * dp[i-1]) % 1000000007 + dp[i-3] % 1000000007) % 1000000007;
        return dp[N-1];
    }
};
```
