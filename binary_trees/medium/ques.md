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
## Maximum Path sum
```
class Solution {
public:
    int solve(TreeNode* root, int& ans){
        if(root==NULL) return 0;
        int lsum = max(0,solve(root->left, ans));
        int rsum = max(0,solve(root->right, ans));
        ans = max(ans, lsum+rsum+root->val);
        return root->val + max(lsum,rsum);
    }
    int maxPathSum(TreeNode* root) {
        int ans = INT_MIN;
        solve(root, ans);
        return ans;
    }
};
```
## Check two trees are identical
```
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p==NULL || q==NULL) return p==q;
        return ( (p->val == q->val) && isSameTree(p->left,q->left) && isSameTree(p->right,q->right) );
    }
};
```
## Zig Zag Traversal
```
class Solution{
    public:
    //Function to store the zig zag order traversal of tree in a list.
    vector <int> zigZagTraversal(Node* root)
    {
    	// Code here
    	vector<int> ans;
    	if(root == NULL) return ans;
    	queue<Node*> q;
    	q.push(root);
    	bool flag = true;
    	while(!q.empty()){
    	    int len = q.size();
    	    vector<int> row(len);
    	    for(int i=0;i<len;i++){
    	        Node* node = q.front();
    	        q.pop();
    	        int index = flag ? i : (len - i -1);
    	        
    	        row[index] = node->data;
    	        if(node->left) q.push(node->left);
    	        if(node->right) q.push(node->right);
    	    }
    	    flag = !flag;
    	   // ans.push_back(row);
    	   for(auto it: row) ans.push_back(it);
    	}
    	return ans;
    }
};
```
## Boundary Traversal
```
class Solution {
  public:
    bool isLeaf(Node* root){
        return (root->left==NULL && root->right==NULL);
    }
    void addLeftBoundary(Node* root, vector<int> &res){
        Node* cur = root->left;
        while(cur){
            if(!isLeaf(cur)) res.push_back(cur->data);
            if(cur->left) cur = cur->left;
            else cur = cur->right;
        }
    }
    void addRightBoundary(Node* root, vector<int> &res){
        Node* cur = root->right;
        vector<int> temp;
        while(cur){
            if(!isLeaf(cur)) temp.push_back(cur->data);
            if(cur->right) cur = cur->right;
            else cur = cur->left;
        }
        for(int i=temp.size()-1;i>=0;i--) res.push_back(temp[i]);
    }
    void addLeaves(Node* root, vector<int> &res){
        if(isLeaf(root)){
            res.push_back(root->data);
            return;
        }
        if(root->left) addLeaves(root->left, res);
        if(root->right) addLeaves(root->right, res);
    }
    vector<int> boundaryTraversal(Node *root) {
        // code here
        vector<int> res;
        if(root==NULL) return res;
        if(!isLeaf(root)) res.push_back(root->data);
        addLeftBoundary(root, res);
        addLeaves(root, res);
        addRightBoundary(root, res);
        return res;
    }
};
```
## Vertical Order Traversal
```
class Solution {
  public:
    vector<vector<int>> verticalOrder(Node *root) {
        // Your code here
        map<int, map<int, multiset<int>> > nodes;
        queue<pair<Node*, pair<int, int>> > todo;
        todo.push({root, {0,0}});
        while(!todo.empty()){
            auto p = todo.front();
            todo.pop();
            Node* node = p.first;
            int x = p.second.first, y = p.second.second;
            nodes[x][y].insert(node->data);
            if(node->left) todo.push({node->left, {x-1,y+1}});
            if(node->right) todo.push({node->right, {x+1,y+1}});
        }
        vector<vector<int>> ans;
        for(auto p: nodes){
            vector<int> col;
            for(auto q: p.second){
                col.insert(col.end(), q.second.begin(), q.second.end());
            }
            ans.push_back(col);
        }
        return ans;
    }
};
```
