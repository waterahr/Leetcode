# 691.贴纸拼词

直觉上依然是一道深搜的题目,以此判断是否可以使用某贴纸达到减少贴纸数量的目的.

```cpp
class Solution {
public:
    int minStickers(vector<string>& stickers, string target) {
        int number = stickers.size();
        vector<vector<int>> mp(number, vector<int>(26, 0));
        map<string, int> dp;
        for(int i=0; i<number; i++)
            for(char c:stickers[i])
                mp[i][c-'a']++;
        dp[""] = 0;
        return dfs(dp, mp, target);
    }
    
private:
    int dfs(map<string, int>& dp, vector<vector<int>>& mp, string target){
        if(dp.find(target) != dp.end()) return dp[target];
        int count = INT_MAX, number = mp.size();
        vector<int> tar(26, 0);
        for(char c:target)
            tar[c-'a']++;
        for(int i=0; i<number; i++){
            // If the target can be spelled out by a group of stickers, at least one of them has to contain character target[0]. So I explicitly require next sticker containing target[0], which significantly reduced the search space.
            if(mp[i][target[0]-'a'] == 0) continue;
            string s;//s is characters target left after using a stick.
            for(int j=0;j<26;j++)
                if(tar[j]-mp[i][j] > 0) 
                    s += string(tar[j]-mp[i][j], 'a'+j);
            //cout<<s<<endl;
            int tmp = dfs(dp, mp, s);
            if(tmp != -1) count = min(count, tmp+1); 
        }
        dp[target] = (count==INT_MAX)?-1:count;
        return dp[target];
    }
};
```
