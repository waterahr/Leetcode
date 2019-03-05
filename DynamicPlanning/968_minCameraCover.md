# 968.监控二叉树

深搜二叉树的每个节点,每个节点有三种状态:已安装监控器、未安装监控器但是可被其他的监控和不可被监控.

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
    int minCameraCover(TreeNode* root) {
        if(!root) return 0;
        int number = 0;
        if(dfs(root, number) == 2) number++;
        return number;
    }
    
private:
    int dfs(TreeNode* root, int& number){
        if(!root)
            return 1;
        int left = dfs(root->left, number), right = dfs(root->right, number);
        if(left == 2 || right == 2){
            number++;
            return 0;
        }else if(left == 0 || right == 0)
            return 1;
        else
            return 2;
    }
};
```
