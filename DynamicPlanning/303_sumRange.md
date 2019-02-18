# 303.区域和检索 - 数组不可变

这是一道简单的动态规划题目，最简单的解法是使用递归直接求解，但是时间复杂度较高。

```cpp
class NumArray {
private:
    vector<int> arr;
public:
    NumArray(vector<int> nums) {
        this->nums = nums;
    }
    
    int sumRange(int i, int j) {
        if(i == j) return nums[i];
        else return nums[i] + sumRange(i+1, j);
    }
};
```

示例中的三次运算，sumRange(0, 5)的计算过程中又一次计算了sumRange(0, 2)、sumRange(2, 5)；即时间的冗余可以通过减少重复的数组遍历来消除。故而，
可以在构造方法中遍历数组一次，保存数组中前i个数值的和到sum[i]中，则sumRange[i, j] = sum[j] - sum[i-1].

```cpp
class NumArray {
private:
    vector<int> sum;
public:
    NumArray(vector<int> nums) {
        //this->nums = nums;
        if(!nums.empty()) sum.push_back(nums[0]);
        for(int i=1; i<nums.size(); i++){
            sum.push_back(arr[i-1] + nums[i]);
        }
    }
    
    int sumRange(int i, int j) {
        /*if(i == j) return nums[i];
        else return nums[i] + sumRange(i+1, j);*/
        if(i==0)
            return sum[j];
        else
            return sum[j] - sum[i-1];
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```
