# 472.连接词

判断一个词是否为连接词可以用动态规划的思路解决,dp[i]表示对于单词s的子串s[:i+1]是否为连接词,状态转移方程为:dp[i]=OR{dp[j]&&s[j+1:i+1] in dict}.

```cpp
class Solution {
public:
    vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
        vector<string> concatennate;
        unordered_set<string> hash(words.begin(), words.end()); 
        for(int i=0; i<words.size(); i++){
            int len = words[i].length();
            if(len == 0) continue;
            vector<bool> dp(len, false);
            dp[0] = hash.find(words[i].substr(0, 1)) != hash.end();
            for(int j=1; j<len; j++){
                if(j+1 != len && hash.find(words[i].substr(0, j+1)) != hash.end()){
                    dp[j] = true;
                    continue;
                }
                for(int k=0; k<j; k++){
                    dp[j] = dp[j] || (dp[k] && (hash.find(words[i].substr(k+1, j-k)) != hash.end()));
                    if(dp[j]) break;
                }
            }
            if(len>1 && dp.back()) concatennate.push_back(words[i]);
        }
        return concatennate;
    }
};
```
