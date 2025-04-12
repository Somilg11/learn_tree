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

