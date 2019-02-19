# 95.不同的二叉搜索树II

与#96相同,dp[i][j]表示区间[i, j]为节点的二叉搜索树的个数,递推关系式为:dp[i][j]=Sigma{dp[i][k-1]*dp[k+1][j]}(i<=k<=j).
不同的是,本题目需要返回生成的二叉树.

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<TreeNode*> generateTrees(int n) {
        vector<TreeNode*> trees;
        if(n == 0) return trees;
        generateTrees(1, n, trees);
        return trees;
    }
    
private:
     void generateTrees(int start, int end, vector<TreeNode*>& trees){
        if(start > end) trees.push_back(NULL);
        for(int i=start; i<=end; i++){
            vector<TreeNode*> left_subtrees, right_subtrees;
            generateTrees(start, i-1, left_subtrees);
            generateTrees(i+1, end, right_subtrees);
            for(auto left:left_subtrees)
                for(auto right:right_subtrees){
                    TreeNode* root = new TreeNode(i);
                    root->left = left;
                    root->right = right;
                    trees.push_back(root);
                }
        }
    }
};
```
