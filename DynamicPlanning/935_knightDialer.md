# 935.骑士拨号器

dp[skip][num]表示从num数字键开始继续跳skip步后生成的数字串的个数,设从num数字键开始时下一步能够跳到的数字键集合为next[num],状态转移方程为:
dp[skip][num]=Sigma{dp[skip-1][next_num]}(next_num in next[num]).

```cpp
class Solution {
public:
    int knightDialer(int N) {
        vector<vector<int>> dp(N, vector<int>(10, 0));
        vector<set<int>> next{{4,6},{6,8},{7,9},{4,8},{0,3,9},{},{0,1,7},{2,6},{1,3},{2,4}};
        for(int i=0; i<10; i++)
            dp[0][i] = 1;
        for(int i=1; i<N; i++)
            for(int j=0; j<10; j++)
                for(int nt:next[j])
                    dp[i][j] = (dp[i][j] % 1000000007 + dp[i-1][nt] % 1000000007) % 1000000007;
        int total = 0;
        for(int i=0; i<10; i++)
            total = (total % 1000000007 + dp[N-1][i]) % 1000000007;
        return total;
    }
};
```
