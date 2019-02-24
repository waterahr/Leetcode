# 576.连续差相同的数字

dp[i]表示i位的连续差相同的数字,则需要考察dp[i-1]中的每个数字是否可以在其后添加一位数字与其个位数字相差K.

```cpp
class Solution {
public:
    vector<int> numsSameConsecDiff(int N, int K) {
        vector<set<int>> dp(N+1);
        if(N==1) dp[1] = {0};
        dp[1].insert({1,2,3,4,5,6,7,8,9});
        for(int i=2; i<=N; i++)
            for(int pre_num:dp[i-1]){
                int add = pre_num % 10 + K;
                if(add < 10)
                    dp[i].insert(pre_num * 10 + add);
                add = pre_num % 10 - K;
                if(add >= 0)
                    dp[i].insert(pre_num * 10 + add);
            }
        vector<int> res;
        for(int num:dp[N])
            res.push_back(num);
        return res;
    }
};
```
