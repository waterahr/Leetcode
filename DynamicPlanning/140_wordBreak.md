# 140.单词拆分II

dp[i]表示s[:i+1]可以拆分成为的句子集合,状态转移方程为:dp[i]=∪{dp[j]+s[j+1:i+1]}(s[j+1:i+1] in dictionary).

```cpp
class Solution {
public:
    vector<string> wordBreak(string s, vector<string>& wordDict) {
        vector<set<string>> dp(s.length()+1);
        unordered_set<string> hash(wordDict.begin(), wordDict.end());
        for(int i=1; i<=s.length(); i++)
            for(int j=0; j<i; j++){
                string tail = s.substr(j, i-j);
                if(hash.find(tail) != hash.end()){
                    if(j==0 && dp[j].size() == 0)
                        dp[i].insert(tail);
                    else
                        for(string pre : dp[j])
                            dp[i].insert(pre+" "+tail);
                }
            }
        vector<string> res(dp.back().begin(), dp.back().end());
        return res;
    }
};
```

超出时间限制,先执行题目139的单词拆分判断true和false,true的话再去找拆分结果就行了.

```cpp
class Solution {
public:
    vector<string> wordBreak(string s, vector<string>& wordDict) {
        vector<set<string>> dp(s.length()+1);
        vector<bool> can(s.length()+1, false);
        unordered_set<string> hash(wordDict.begin(), wordDict.end());
        can[0] = true;
        for(int i=1; i<=s.length(); i++)
            for(int j=0; j<i; j++){
                string tail = s.substr(j, i-j);
                if(hash.find(tail) != hash.end())
                    can[i] = can[i] || can[j];
                if(can[i]) break;
            }
        if(!can.back()) return {};
        for(int i=1; i<=s.length(); i++){
            if(!can[i]) continue;
            for(int j=0; j<i; j++){
                string tail = s.substr(j, i-j);
                if(hash.find(tail) != hash.end()){
                    if(j==0 && dp[j].size() == 0)
                        dp[i].insert(tail);
                    else
                        for(string pre : dp[j])
                            dp[i].insert(pre+" "+tail);
                }
            }
        }
        vector<string> res(dp.back().begin(), dp.back().end());
        return res;
    }
};
```
