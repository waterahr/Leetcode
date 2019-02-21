# 139.单词拆分

dp[i]表示字符串s[:i]是否可以被空格拆分为一个或多个字典中的单词,递推关系式为:dp[i]=Or{dp[j] and (s[j:i] in wordDic)}(0<=j<i).


```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<bool> dp(s.length()+1, false);
        unordered_set<string> dict;
        for(string word:wordDict)
            dict.insert(word);
        dp[0] = true;
        for(int i=1; i<=s.length(); i++)
            for(int j=0; j<i; j++){
                dp[i] = dp[i] || (dp[j] && (dict.find(s.substr(j, i-j)) != dict.end()));
                if(dp[i]) break;
            }
        return dp.back();
    }
};
```
