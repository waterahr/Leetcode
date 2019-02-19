# 638.大礼包

针对每个大礼包，计算使用这个礼包后的花费，如果比当前的最低花费少， 则更新最小化非为使用礼包后的花费;
因为题目要求不可以购买超出待购清单的物品,显然这里需要考虑的一个问题就是回溯.

```cpp
class Solution {
public:
    bool checkvalid(vector<int>& needs, const vector<int>& special) {
        for(int j = 0; j<needs.size(); j++)
            if(needs[j] < special[j]) return false;
        return true;
    }
    int shoppingOffers(vector<int>& price, vector<vector<int>>& special, vector<int>& needs){
        int minPrice = 0;
        for (int i = 0; i<needs.size(); i++) {
            minPrice += needs[i] * price[i];
        }
       
        for (int i = 0; i<special.size(); i++) {
            if(checkvalid(needs, special[i])){
                vector<int> curNeeds;
                for (int j = 0; j<needs.size(); j++) {
                    curNeeds.push_back(needs[j] - special[i][j]);
                }
                int tempPrice = shoppingOffers(price, special, curNeeds) + special[i][needs.size()];
                minPrice = min(minPrice, tempPrice);
            }
        }

        return minPrice;
    }
};
```
