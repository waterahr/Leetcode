# 740.删除与获得点数

dp[i]表示到达nums[i]时可以获得的最大点数,因为不同的数值可能有多个,所以需要建立数值及其在数组中出现次数的映射,最简单高效的方法就是用数组的下标实现,
有递推关系式:dp[i]=max(dp[i-1], dp[i-2]+nums[i]*count[nums[i]).

```cpp
class Solution {
public:
    int deleteAndEarn(vector<int>& nums) {
        if(nums.size() == 0) return 0;
        sort(nums.begin(), nums.end());
        int max_value = nums.back() + 1;
        vector<int> count(max_value, 0), dp(max_value, 0);
        for(int num:nums)
            count[num]++;
        dp[1] = 1 * count[1];
        for(int i=2; i<max_value; i++)
            dp[i] = max(dp[i-1], dp[i-2] + i * count[i]);
        return dp[max_value-1];
    }
};
```
