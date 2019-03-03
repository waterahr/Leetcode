# 79.交错字符串

dp[i][j]表示s1[:i]、s2[:j]是否构成交错字符串s3[:i+j],状态转移方程为:
dp[i][j]=OR{dp[i-1][j]&&s1[i-1]==s3[i+j-1], dp[i][j-1]&&s2[j-1]==s3[i+j-1]}.

```cpp
class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {
        if(s3.length() != s1.length()+s2.length()) return false;
        vector<vector<bool>> dp(s1.length()+1, vector<bool>(s2.length()+1, false));
        dp[0][0] = true;
        for(int i=0;i<=s1.length();i++){
            for(int j=0;j<=s2.length();j++){
                if(i!=0 && s3[i+j-1] == s1[i-1] && dp[i-1][j])
                    dp[i][j] = true;
                if(j!=0 && s3[i+j-1] == s2[j-1] && dp[i][j-1])
                    dp[i][j] = true;
            }
        }
        return dp[s1.length()][s2.length()];
    }
};
```
