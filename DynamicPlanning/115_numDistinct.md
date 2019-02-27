# 115.不同的子序列

dp[i][j]表示s[:i]中t[:j]出现的次数,状态转移方程为:
s[i-1]==t[j-1]?dp[i][j]=dp[i-1][j]+dp[i-1][j-1];s[-1]!=t[j-1]?dp[i][j]=dp[i-1][j].

```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        vector<vector<long>> dp(s.length()+1, vector<long>(t.length()+1, 0));
        for(int i=0; i<=s.length(); i++)
            dp[i][0] = 1;
        for(int i=1; i<=s.length(); i++)
            for(int j=1; j<=t.length(); j++){
                if(s[i-1] == t[j-1])
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                else
                    dp[i][j] = dp[i-1][j];
            }
        return dp[s.length()][t.length()];
    }
};
```
