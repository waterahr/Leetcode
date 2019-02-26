# 898.子数组按位或操作

用record记录以nums[i-1]结尾的连续子数组的按位或操作的所有计算结果,状态转移方程为:cur.insert(nums[i]|x)(x in record).

```cpp
class Solution {
public:
    int subarrayBitwiseORs(vector<int>& A) {
        set<int> record;
        set<int> ans;

        for(int i = 0; i < A.size(); ++i)
        {
            set<int> cur;
            for(int x : record) cur.insert(x | A[i]);
            cur.insert(A[i]);
            record = cur;

            ans.insert(cur.begin(), cur.end());
        }

        return ans.size();
    }
};
```
