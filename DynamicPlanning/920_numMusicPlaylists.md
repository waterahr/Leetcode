# 920.播放列表的数量

dp[i][j]表示用j首歌,覆盖前i个位置方案数,这里注意不是前j首歌,而是n个里面的任意j首,这和一些经典思路还是不太一样的;
状态转移方程为:dp[i][j]=dp[i−1][j−1]*(n−j+1)+dp[i−1][j]*max(j−k, 0).第一项表示第i个位置要放新歌了,
可以是除了前j-1首的任意一首;第二项表示,前i-1个位置已经放了j首歌了,第i个位置可以从前j首歌里选,但是要选之前的k首歌不一样的.

```cpp
class Solution {
public:
    int numMusicPlaylists(int N, int L, int K) {
        long MOD = 1e9+7;
        vector<long> dp(N + 1);
        dp[0] = 1;
        for (int i = 1; i <= L; i++){
            for (int j = min(N, i); j > 0; j--){
                dp[j] = (dp[j-1] * (N - j + 1) + dp[j] * max(j - K, 0)) % MOD;
            }
            dp[0] = 0;
        }
        return dp[N];
    }
};
```
