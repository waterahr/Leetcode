# 392.判断子序列

dp[i][j]表示s[:i]是否为t[:j]的子序列（j>=i）,递推关系式为:
dp[i][j]=Or{dp[i-1][k-1] and s[i]==t[k]}(i<=k<=j).

```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int len_s = s.length(), len_t = t.length();
        if(len_s == 0) return true;
        if(len_t == 0) return false;
        vector<vector<bool>> dp(len_s+1, vector<bool>(len_t+1, false));
        for(int i=0; i<=len_t; i++)
            dp[0][i] = true;
        dp[1][1] = s[0]==t[0];
        for(int i=1; i<=len_s; i++)
            for(int j=1; j<=len_t; j++)
                for(int k=i; k<=j; k++){
                    dp[i][j] =dp[i][j] || (dp[i-1][k-1] && (s[i-1]==t[k-1]));
                    if(dp[i][j]) break;
                }
        return dp[len_s][len_t];
    }
};
```

太可惜了,超出时间限制!放弃使用动态规划的思路进行求解,使用双指针解题.

```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int len_s = s.length(), len_t = t.length();
        int i=0, j=0;
        for(; i<len_s && j<len_t; ){
            if(s[i] == t[j]){
                i++; j++;
            }else
                j++;
        }
        return i==len_s;
    }
};
```
