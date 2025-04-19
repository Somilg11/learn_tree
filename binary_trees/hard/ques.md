## Print root to node path in  binary tree
```
class Solution {
  public:
    bool solve(Node* root, vector<int>&arr, int x){
        if(!root) return false;
        arr.push_back(root->data);
        if(root->data==x) return true;
        if(solve(root->left, arr, x) || solve(root->right, arr, x)) return true;
        arr.pop();
        return false;
    }
    vector<int> Paths(Node* root, int target) {
        // code here
        vector<int> arr;
        if(root==NULL) return;
        solve(root, arr, target);
        return arr;
    }
};
```
## Lowest common ancestor
```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == NULL || root == p || root == q) return root;
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if(left == NULL) return right;
        else if(right == NULL) return left;
        else return root;
    }
};
```
## Maximum width of binary tree
```
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if(!root) return 0;
        long long ans = 0;
        queue<pair<TreeNode*,long long>> q;
        q.push({root, 0});
        while(!q.empty()){
            long long size = q.size();
            long long mini = q.front().second;
            long long first, last;
            for(long long i=0;i<size;i++){
                long long cur_id = q.front().second - mini;
                TreeNode* node = q.front().first;
                q.pop();
                if(i==0) first=cur_id;
                if(i==size-1) last=cur_id;
                if(node->left) q.push({node->left, cur_id*2+1});
                if(node->right) q.push({node->right, cur_id*2+2});
            }
            ans = max(ans, last-first+1);
        }
        return ans;
    }
};
```