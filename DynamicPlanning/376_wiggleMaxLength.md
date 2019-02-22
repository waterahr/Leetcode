# 376.摆动序列

dp_greater[i]表示以nums[i]结尾的最后一个差值大于0的最长摆动序列的长度, dp_less[i]表示以nums[i]结尾的最后一个差值小于0的最长摆动序列的长度,
递推关系式为:nums[i]>nums[j]?dp_greater[i]=max{dp_less[j]+1}(0<=j<i);nums[i]<nums[j]?dp_less[i]=max{dp_greater[j]+1}(0<=j<i).

```cpp
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        if(nums.size() == 0) return 0;
        vector<int> dp_greater(nums.size(), 1), dp_less(nums.size(), 1);
        int max_len = 1;
        for(int i=1; i<nums.size(); i++){
            for(int j=0; j<i; j++){
                if(nums[i] > nums[j])
                    dp_greater[i] = max(dp_greater[i], dp_less[j] + 1);
                else if(nums[i] < nums[j])
                    dp_less[i] = max(dp_less[i], dp_greater[j] + 1);
                else
                    continue;
            }
            max_len = max(max(dp_greater[i], dp_less[i]), max_len);
        }
        return max_len;
    }
};
```
