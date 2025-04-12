
# 🌳 Trees in Data Structures and Algorithms (DSA)

## 📘 Introduction

A **Tree** is a hierarchical data structure that simulates a tree-like structure with a set of connected nodes. Unlike linear data structures (like arrays, stacks, queues, and linked lists), a tree can represent complex relationships such as hierarchy and parent-child connections.

- The **topmost node** is called the **Root**.
- Every node (except the root) has one **parent** and zero or more **children**.
- A **Tree** is a special type of **Graph** with no cycles.

### 🔑 Key Terminologies

| Term            | Description |
|-----------------|-------------|
| Root            | The topmost node in the tree |
| Node            | Element in a tree |
| Edge            | Connection between parent and child |
| Leaf            | A node with no children |
| Parent          | A node that has one or more children |
| Child           | A node that descends from another node |
| Subtree         | A tree formed from a node and its descendants |
| Height          | Longest path from root to a leaf |
| Depth/Level     | Distance from the root node |

## 🌲 Types of Trees

### 1. **General Tree**
- Each node can have any number of children.
- No restriction on structure.

### 2. **Binary Tree**
- Each node can have at most **two children**.
- Common types:
  - **Full Binary Tree**: Every node has 0 or 2 children.
  - **Perfect Binary Tree**: All internal nodes have two children and all leaves are at the same level.
  - **Complete Binary Tree**: All levels are completely filled except possibly the last, which is filled from left to right.
  - **Skewed Binary Tree**: All nodes are aligned to one side (left or right).

### 3. **Binary Search Tree (BST)**
- A binary tree with the property:  
  For any node,
  ```
  Left subtree nodes < Root < Right subtree nodes
  ```
- Efficient for searching, insertion, and deletion (Average Time: O(log n)).

### 4. **AVL Tree (Self-Balancing BST)**
- A BST with a balancing condition:  
  The height difference between left and right subtree is at most 1.
- Ensures O(log n) time for search, insert, delete.

### 5. **Red-Black Tree**
- A self-balancing BST with an extra bit for color (Red or Black).
- Balancing rules:
  - Root is always black.
  - No two red nodes can be adjacent.
  - Every path from root to leaf has the same number of black nodes.

### 6. **B Tree**
- Generalization of BST where a node can have more than two children.
- Used in databases and file systems for handling large blocks of data.

### 7. **Heap Tree**
- A **Complete Binary Tree** that satisfies the **Heap Property**:
  - **Max Heap**: Parent node ≥ children
  - **Min Heap**: Parent node ≤ children

### 8. **Trie (Prefix Tree)**
- Special tree used to store strings.
- Each node represents a character of the word.
- Used for efficient searching (like autocomplete).

### 9. **Segment Tree**
- Used for storing intervals or segments.
- Allows querying and updating ranges in logarithmic time.

### 10. **Fenwick Tree (Binary Indexed Tree)**
- Similar to segment tree, used for prefix sum queries efficiently.

## 📌 Use Cases of Trees
- **Binary Search Tree** – Searching and sorting
- **Heaps** – Priority queues
- **Tries** – Spell checking, IP routing, search engines
- **Segment Trees/Fenwick Trees** – Range queries and updates
- **B Trees** – Database indexing
