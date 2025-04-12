## Binary tree representation
```cpp
#include <iostream>
using namespace std;

// Definition of a binary tree node
struct Node {
    int data;
    Node* left;
    Node* right;

    // Constructor
    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

// Function to create a new node
Node* createNode(int value) {
    return new Node(value);
}

// Example usage
int main() {
    // Creating the root node
    Node* root = createNode(1);

    // Adding child nodes
    root->left = createNode(2);
    root->right = createNode(3);

    cout << "Root Node: " << root->data << endl;
    cout << "Left Child: " << root->left->data << endl;
    cout << "Right Child: " << root->right->data << endl;

    return 0;
}
```
## Traversal techniques - BFS | DFS
- inorder ( LEFT ROOT RIGHT )
- preorder ( ROOT LEFT RIGHT )
- postorder ( LEFT RIGHT ROOT )

### Preorder traversal
```
class Solution {
  public:
    void solve(Node* root, vector<int> &ans){
        if(root == NULL) return;
        ans.push_back(root->data);
        solve(root->left, ans);
        solve(root->right, ans);
    }

    // Function to return a list containing the preorder traversal of the tree.
    vector<int> preorder(Node* root) {
        // write code here
        vector<int> ans;
        solve(root, ans);
        return ans;
    }
};
```
### Post order traversal
```
class Solution {
  public:
    void solve(Node* root, vector<int> &ans){
        if(root==NULL) return;
        solve(root->left, ans);
        solve(root->right, ans);
        ans.push_back(root->data);
    }
    // Function to return a list containing the postorder traversal of the tree.
    vector<int> postOrder(Node* root) {
        // Your code here
        vector<int> ans;
        solve(root, ans);
        return ans;
    }
};
```
### Level order traversal
```
class Solution {
  public:
    // Function to return the level order traversal line by line of a tree.
    vector<vector<int>> levelOrder(Node* root) {
        // Your code here
        vector<vector<int>> ans;
        if(root==NULL) return ans;
        queue<Node*> q;
        q.push(root);
        while(!q.empty()){
            int n = q.size();
            vector<int> level;
            for(int i=0;i<n;i++){
                Node* node = q.front();
                q.pop();
                if(node->left!=NULL) q.push(node->left);
                if(node->right!=NULL) q.push(node->right);
                level.push_back(node->data);
            }
            ans.push_back(level);
        }
        return ans;
    }
};
```
### Preorder with stack
```
vector<int> preorder(Node* root) {
        // write code here
        vector<int> ans;
        if(root==NULL) return ans;
        stack<Node*> st;
        st.push(root);
        while(!st.empty()){
            Node* node = st.top();
            st.pop();
            ans.push_back(node->data);
            if(node->right!=NULL) st.push(node->right);
            if(node->left!=NULL) st.push(node->left);
        }
        return ans;
    }
```
### Inorder with stack
```
vector<int> inOrder(Node* root) {
        // Your code here
        stack<Node*> st;
        Node* node = root;
        vector<int> ans;
        while(true){
            if(node!=NULL){
                st.push(node);
                node = node->left;
            } else {
                if(st.empty()) break;
                node = st.top();
                st.pop();
                ans.push_back(node->data);
                node = node->right;
            }
        }
        return ans;
    }
```
### postorder using 2 stacks
```
vector<int> postOrder(Node* root) {
        // Your code here
        vector<int> ans;
        if(root==NULL)return ans;
        stack<Node*> st1, st2;
        st1.push(root);
        while(!st.empty()){
            root = st.top();
            st1.pop();
            st2.push(root);
            if(root->left!=NULL) st1.push(root->left);
            if(root->right!=NULL) st1.push(root->right);
        }
        while(!st2.empty()){
            ans.push_back(st2.top()->data);
            st2.pop();
        }
        return ans;
    }
```