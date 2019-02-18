# 877.石子游戏

类似的题目有一个规律:总是先手赢得游戏.使用动态规划解题,dp[i][j]表示下标i\~j之间的石堆进行游戏时先手的人比后手的人多拿的石子,递推关系式为:
dp[i][j]=max(piles[i]-dp[i+1][j], piles[j]-dp[i][j-1]).

```cpp
class Solution {
public:
    bool stoneGame(vector<int>& piles) {
        vector<vector<int>> dp(piles.size(), vector<int>(piles.size(), 0));
        for(int i=0; i<piles.size(); i++)
            dp[i][i] = piles[i];
        for(int i=piles.size()-1; i>=0; i--){
            for(int j=i+1; j<piles.size(); j++){
                dp[i][j] = max(piles[i] - dp[i+1][j], piles[j] - dp[i][j-1]);
            }
        }
        return dp[0][piles.size()-1] > 0;
    }
};
```
