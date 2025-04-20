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
## children sum property
```
void isSumProperty(Node *root)
    {
     // Add your code here
     if(root==NULL) return;
     int child = 0;
     if(root->left) child+=root->left->data;
     if(root->right) child+=root->right->data;
     if(child >= root->data) root->data=child;
     else{
        if(root->left) root->left->data=root->data;
        else if(root->right) root->right->data=root->data;
     }
     reorder(root->left);
     reorder(root->right);
     int tot = 0;
     if(root->left) tot+=root->left->data;
     if(root->right) tot+=root->right->data;
     if(root->left || root->right) root->data=tot;
    }
```
## Nodes at a distance K
```
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
    void markParents(TreeNode* root, unordered_map<TreeNode*, TreeNode*>& parents) {
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            TreeNode* curr = q.front(); q.pop();
            if (curr->left) {
                parents[curr->left] = curr;
                q.push(curr->left);
            }
            if (curr->right) {
                parents[curr->right] = curr;
                q.push(curr->right);
            }
        }
    }
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        unordered_map<TreeNode*, TreeNode*> parents;
        markParents(root, parents);

        unordered_map<TreeNode*, bool> vis;
        queue<TreeNode*> q;
        q.push(target);
        vis[target] = true;

        int dist = 0;
        while (!q.empty()) {
            if (dist == k) break;
            int size = q.size();
            dist++;
            for (int i = 0; i < size; ++i) {
                TreeNode* curr = q.front(); q.pop();
                if (curr->left && !vis[curr->left]) {
                    vis[curr->left] = true;
                    q.push(curr->left);
                }
                if (curr->right && !vis[curr->right]) {
                    vis[curr->right] = true;
                    q.push(curr->right);
                }
                if (parents[curr] && !vis[parents[curr]]) {
                    vis[parents[curr]] = true;
                    q.push(parents[curr]);
                }
            }
        }

        vector<int> res;
        while (!q.empty()) {
            res.push_back(q.front()->val);
            q.pop();
        }
        return res;
    }
};
```