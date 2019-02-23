# 152.乘积最大子序列

dp_max[i]表示数组nums[:i+1]中的子序列的最大乘积,dp_min[i]表示数组nums[:i+1]中的子序列的最小乘积,状态转移方程为:
dp_max[i]=max(nums[i], nums[i]*dp_max[i-1], nums[i]*dp_min[i-1]);dp_min[i]=min(nums[i], nums[i]*dp_max[i-1], nums[i]*dp_min[i-1]).

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        vector<int> dp_max(nums.size(), INT_MIN), dp_min(nums.size(), INT_MAX);
        dp_max[0] = nums[0];
        dp_min[0] = nums[0];
        int max_value = dp_max[0];
        for(int i=1; i<nums.size(); i++){
            dp_max[i] = max({nums[i], nums[i] * dp_max[i-1], nums[i] * dp_min[i-1]});
            dp_min[i] = min({nums[i], nums[i] * dp_max[i-1], nums[i] * dp_min[i-1]});
            max_value = max(max_value, dp_max[i]);
        }
        return max_value;
    }
};
```
