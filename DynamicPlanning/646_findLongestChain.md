# 646.最长数对链

dp[i]表示以pairs[i]结尾的最长数对链的长度,递推关系式为:dp[i]=max{dp[j]+1}(0<=j<=i-1, pairs[j][1]<pairs[i][0]).

```cpp
class Solution {
public:
    int findLongestChain(vector<vector<int>>& pairs) {
        sort(pairs.begin(), pairs.end());
        vector<int> dp(pairs.size(), 1);
        int max_len = 0;
        for(int i=0; i<pairs.size(); i++){
            for(int j=0; j<i; j++)
                if(pairs[j][1] < pairs[i][0])
                    dp[i] = max(dp[i], dp[j]+1);
            max_len = max(max_len, dp[i]);
        }
        return max_len;
    }
};
```
