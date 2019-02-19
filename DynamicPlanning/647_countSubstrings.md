# 647.回文子串

dp[i][j]表示字符串s[i:j+1]中的回文子串的个数,递推关系式为:
s[i]\~s[j]构成回文串=>dp[i][j]=dp[i][j-1]+dp[i+1][j]-dp[i+1][j-1]+1;
s[i]\~s[j]不构成回文串=>dp[i][j]=dp[i][j-1]+dp[i+1][j]-dp[i+1][j-1].

```cpp
class Solution {
public:
    int countSubstrings(string s) {
        int len = s.length();
        vector<vector<int>> dp(len, vector<int>(len, 0));
        for(int i=0; i<len; i++)
            dp[i][i] = 1;
        for(int i=len-1; i>=0; i--)
            for(int j=i+1; j<len; j++){
                dp[i][j] = dp[i][j-1] + dp[i+1][j] - dp[i+1][j-1];
                if(huiwen(s.substr(i, j-i+1))) dp[i][j]++;
            }
        return dp[0][len-1];
    }
    
private:
    bool huiwen(string s){
        int len = s.length();
        for(int i=0; i<len/2; i++)
            if(s[i] != s[len-1-i]) return false;
        return true;
    }
};
```
