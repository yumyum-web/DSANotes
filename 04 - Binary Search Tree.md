# Tree

- **Tree** is a connected graph with no cycles.
- **Rooted tree** has a designated root node, and every edge is directed away from the root.
- **Binary tree** is a rooted tree where each node has at most two children.
- **Binary search tree (BST)** is a binary tree where the left subtree of a node contains only nodes with keys less than
  the node's key, and the right subtree contains only nodes with keys greater than the node's key.

## Rooted Tree

- **Root**: The topmost node in a tree.
- **Node**: A single element in a tree.
- **Edge**: A connection between two nodes.
- **Path**: A sequence of nodes where each node is connected to the next.

[//]: # ()

- **Parent**: A node is a parent of its children.
- **Child**: A node is a child of its parent.
- **Siblings**: Nodes with the same parent.

[//]: # ()

- **Internal Node**: A node with children.
- **External Node (Leaf)**: A node with no children.

[//]: # ()

- **Degree**: The number of children a node has.
- **Depth**: The number of edges from the root to the node.
- **Height**: The number of edges on the longest path from the node to a leaf.

[//]: # ()

- **Level**: All nodes at the same depth.
- **Complete Tree**: A tree where all levels are filled except possibly the last level, which is filled from left
  to right.

[//]: # ()

- **Subtree**: A tree rooted at a node.
- **Ancestor**: An ancestor of a node is a node on the path from the root to the node.
    - **Proper Ancestor**: An ancestor that is not the node itself.
- **Descendant**: A descendant of a node is a node in the subtree rooted at the node.
    - **Proper Descendant**: A descendant that is not the node itself.

[//]: # ()

- **Forest**: A collection of disjoint trees.

## Binary Tree

### Traversal

- **Preorder**: Visit the root node first, then recursively visit the left and right subtrees.
- **Inorder**: Recursively visit the left subtree, then visit the root node, then recursively visit the right subtree.
- **Postorder**: Recursively visit the left and right subtrees, then visit the root node.

## Binary Search Tree (BST)

- This is an abstract data type (ADT) that stores items in a tree.
- Every left descendant of a node has a value less than the node's value and every right descendant has a value greater
  than the node's value.
- BST operations:
    - **Create**: Create a new instance of the tree.
    - **Insert**: Add a new node to the tree.
    - **Search**: Find a node with a given value.
    - **Delete**: Remove a node from the tree.
    - **Traverse**: Visit all nodes in the tree.
- Other operations:
    - **Minimum**: Find the node with the smallest value.
    - **Maximum**: Find the node with the largest value.
    - **Successor**: Find the node with the next larger value.
    - **Predecessor**: Find the node with the next smaller value.
    - **Height**: Find the height of the tree.
    - **Balance**: Check if the tree is balanced.
- In-order traversal of a BST produces a sorted sequence of values.

### Insertion

1. If the tree is empty, create a new node and set it as the root.
2. Otherwise, start at the root and:
    - If the new value is less than the current node's value, go left.
    - If the new value is greater than the current node's value, go right.
    - If the current node is null, insert the new node.

- Time complexity: $O(h)$, where $h$ is the height of the tree.

### Searching

- Start at the root and:
    - If the value is equal to the current node's value, return the node.
    - If the value is less than the current node's value, go left.
    - If the value is greater than the current node's value, go right.
    - If the current node is null, return null.
- Time complexity: $O(h)$, where $h$ is the height of the tree.

### Deletion

- Three cases:
    1. Node has no children: Remove the node.
    2. Node has one child: Replace the node with its child.
    3. Node has two children: Find the successor, replace the node with the inorder successor or predecessor.
- Time complexity: $O(h)$, where $h$ is the height of the tree.
- **Successor:** The leftmost child of the right subtree (The smallest value from larger values).
- **Predecessor:** The rightmost child of the left subtree (The largest value from smaller values).

### Balancing

- **Balanced Tree**: A tree where the height of the left and right subtrees of every node differ by at most one.
- A balanced tree has a height of $O(log n)$, where $n$ is the number of nodes. It is the _minimum height_ for a tree
  with $n$ nodes.
- An unbalanced tree is undesirable because it can lead to inefficient operations.
- There are several binary tree types that maintain balance, _e.g., AVL tree, Red-Black tree, etc._