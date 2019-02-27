# 982.按位与为零的三元组

```cpp
class Solution {
public:
    int countTriplets(vector<int>& A) {
        int sum = 0;
        map<int, int> m;
		for(int a:A)
			for (int b:A){
                int res = a & b;
                m[res] += 1;
                //cout<<res<<' '<<m[res]<<endl;
            }
        for(auto iter=m.begin(); iter!=m.end(); iter++)
            for(int a:A)
                if(((iter->first) & a) == 0){
                    sum += iter->second;
                }
		return sum;
    }
};
```
