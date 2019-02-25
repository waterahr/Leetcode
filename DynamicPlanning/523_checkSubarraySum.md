# 523.连续的子数组和

```cpp
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        if(nums.size() < 2) return false;
        for(int i=0; i<nums.size()-1; i++)
            if(!nums[i] && !nums[i+1]) return true;
        if(!k) return false;
        if(k < 0) k = -k;
        
        map<int, int> m;
        m[0] = -1;
        int sum = 0;
        int i=0;
        for(int num:nums){
            sum += num;
            int mod =  sum % k;
            if(m.find(mod) != m.end()){
                if(i++ - m[mod] > 1) return true;
            }
            else
                m[mod] = i++;
        }
        return false;
    }
};
```
