# 494.目标和

dp[t][i]表示使用区间[0, i]之间的数字组成目标t的添加符号的方法个数,递推关系式为:dp[t][i]=dp[t-nums[i]][i-1]+dp[t+nums[i]][i-1].

```cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        vector<vector<int>> dp(2001, vector<int>(nums.size(), 0));
        dp[nums[0]+1000][0] += 1;
        dp[1000-nums[0]][0] += 1;
        int sum = 0;
        for(int num:nums)
            sum += abs(num);
        if(S > sum || S < -sum)
            return 0;
        
        for(int i=1; i<nums.size(); i++)
            for(int j=-1000; j<1000; j++){
                if(j-nums[i]+1000 >= 0 && j-nums[i]+1000 < 2000) 
                    dp[j+1000][i] += dp[j-nums[i]+1000][i-1];
                if(j+nums[i]+1000 >= 0 && j+nums[i]+1000 < 2000) 
                    dp[j+1000][i] += dp[j+nums[i]+1000][i-1];
            }
        return dp[S+1000][nums.size()-1];
    }
};
```
