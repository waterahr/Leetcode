# 354.俄罗斯套娃信封问题

dp[i]表示最外层信封为envelopes[i]时的最多信封数,状态转移方程为:
```
dp[i]=max{dp[j]+1}(j<i, envelpes[i]>envelopes[j]).
```

```cpp
class Solution {
public:
    int maxEnvelopes(vector<pair<int, int>>& envelopes) {
        int n = envelopes.size();
        if(n == 0) return 0;
        sort(envelopes.begin(), envelopes.end());
        vector<int> dp(n, 1);
        int count = 1;
        for(int i=1; i<n; i++){
            for(int j=0; j<i; j++)
                if(envelopes[i].first > envelopes[j].first && envelopes[i].second > envelopes[j].second)
                    dp[i] = max(dp[i], dp[j] + 1);
            count = max(count, dp[i]);
        }
        return count;
    }
};
```
