## Height of Binary tree
```
class Solution {
  public:
    // Function to find the height of a binary tree.
    int height(struct Node* node) {
        // code here
        if(node==NULL) return -1;
        return max(height(node->left),height(node->right)) + 1;
    }
};
```
## Check balance binary tree
```
class Solution {
public:
    int check(TreeNode* node){
        if(node==NULL) return 0;
        int lh = check(node->left);
        if(lh==-1) return -1;
        int rh = check(node->right);
        if(rh==-1) return -1;
        if(abs(lh-rh)>1) return -1;
        return max(lh,rh)+1;
    }
    bool isBalanced(TreeNode* root) {
        if(check(root) != -1) return true;
        else return false;
    }
};
```
## Diameter of Binary tree
```
class Solution {
public:
    int check(TreeNode* root, int &ans){
        if(root==NULL) return 0;
        int left = check(root->left, ans);
        int right = check(root->right, ans);
        ans = max(left+right,ans);
        return 1+max(left,right);
    }
    int diameterOfBinaryTree(TreeNode* root) {
        int ans = 0;
        check(root, ans);
        return ans;
    }
};
```