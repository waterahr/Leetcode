# 5.最长回文子串

dp[i][j]表示字符串s[i:j+1]是否为回文子串,状态转移方程为:dp[i][j]=dp[i+1][j-1]&&s[i]==s[j].

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        vector<vector<bool>> dp(s.length(), vector<bool>(s.length(), false));
        int start = 0, end = 0;
        for(int i=s.length()-1; i>=0; i--){
            dp[i][i] = true;
            for(int j=i+1; j<s.length(); j++){
                dp[i][j] = (j < i+2 || dp[i+1][j-1]) && s[i]==s[j];
                if(dp[i][j] && j - i > end - start){
                    start = i;
                    end = j;
                }
            }
        }
        return s.substr(start, end-start+1);
    }
};
```
