### **Trees in Python**

#### **Description**
A tree is a hierarchical data structure that consists of nodes connected by edges. Trees are an extension of linked lists where each node can have multiple children. The topmost node is called the root, and every node (except the root) is connected by a directed edge from exactly one other node, known as its parent. Nodes with no children are called leaves.

Trees are widely used in computer science for representing hierarchical data such as file systems, organization structures, and abstract syntax trees. They are also used in algorithms like searching, sorting, and traversing data structures.

#### **Types of Trees**

##### **Binary Tree**
- **Description**: A binary tree is a type of tree where each node has at most two children, often referred to as the left child and the right child.

##### **Binary Search Tree (BST)**
- **Description**: A binary search tree is a binary tree with an additional property: for any given node, all the nodes in its left subtree have values less than the node’s value, and all the nodes in its right subtree have values greater than the node’s value. This property makes BSTs particularly efficient for searching, insertion, and deletion operations.

### **Basic Tree Operations**

To better understand trees, we’ll implement a simple binary search tree (BST) in Python.

#### **Node Class**
The `Node` class represents each element (or node) in the tree.

```python
class Node:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.val = key
```

#### **Binary Search Tree (BST) Implementation**
Here’s how you might implement the basic operations for a binary search tree:

##### **Insertion**
Insertion in a BST involves adding a new node in such a way that the BST property is maintained. The insertion operation is done recursively:

```python
def insert(self, key):
    if self.val:
        if key < self.val:
            if self.left is None:
                self.left = Node(key)
            else:
                self.left.insert(key)
        elif key > self.val:
            if self.right is None:
                self.right = Node(key)
            else:
                self.right.insert(key)
    else:
        self.val = key

# Example usage
root = Node(10)
root.insert(5)
root.insert(20)
root.insert(3)
root.insert(7)
root.insert(15)
```

##### **Deletion**
Deleting a node from a BST can be a bit complex. The process differs based on whether the node to be deleted has no children (leaf node), one child, or two children:

1. **Node with No Children**: Simply remove the node.
2. **Node with One Child**: Remove the node and link its parent to its child.
3. **Node with Two Children**: Find the in-order successor (smallest node in the right subtree), replace the node with the in-order successor, and delete the successor node.

Here’s a basic implementation:

```python
def delete_node(self, root, key):
    if root is None:
        return root

    # If the key to be deleted is smaller than the root's key
    if key < root.val:
        root.left = self.delete_node(root.left, key)

    # If the key to be deleted is greater than the root's key
    elif key > root.val:
        root.right = self.delete_node(root.right, key)

    # If key is same as root's key, this is the node to be deleted
    else:
        # Node with only one child or no child
        if root.left is None:
            return root.right
        elif root.right is None:
            return root.left

        # Node with two children: Get the inorder successor (smallest in the right subtree)
        temp = self.min_value_node(root.right)

        # Copy the inorder successor's content to this node
        root.val = temp.val

        # Delete the inorder successor
        root.right = self.delete_node(root.right, temp.val)

    return root

def min_value_node(self, node):
    current = node
    while current.left is not None:
        current = current.left
    return current

# Example usage
root = root.delete_node(root, 10)
```

##### **Traversal**
Traversal means visiting all the nodes in the tree. There are several ways to traverse a binary tree, each serving different purposes:

- **In-order Traversal (Left, Root, Right)**: This traversal method visits the left subtree, then the root, and finally the right subtree. For BSTs, in-order traversal visits nodes in ascending order.

```python
def inorder_traversal(self, root):
    res = []
    if root:
        res = self.inorder_traversal(root.left)
        res.append(root.val)
        res = res + self.inorder_traversal(root.right)
    return res

# Example usage
print(root.inorder_traversal(root))  # Output: [3, 5, 7, 15, 20]
```

- **Pre-order Traversal (Root, Left, Right)**: This traversal method visits the root first, then the left subtree, and finally the right subtree.

```python
def preorder_traversal(self, root):
    res = []
    if root:
        res.append(root.val)
        res = res + self.preorder_traversal(root.left)
        res = res + self.preorder_traversal(root.right)
    return res

# Example usage
print(root.preorder_traversal(root))  # Output: [10, 5, 3, 7, 20, 15]
```

- **Post-order Traversal (Left, Right, Root)**: This traversal method visits the left subtree first, then the right subtree, and finally the root.

```python
def postorder_traversal(self, root):
    res = []
    if root:
        res = self.postorder_traversal(root.left)
        res = res + self.postorder_traversal(root.right)
        res.append(root.val)
    return res

# Example usage
print(root.postorder_traversal(root))  # Output: [3, 7, 5, 15, 20, 10]
```

- **Level-order Traversal**: This traversal method visits nodes level by level, starting from the root. It typically uses a queue data structure.

```python
def level_order_traversal(self, root):
    res = []
    queue = []
    if root:
        queue.append(root)

    while queue:
        node = queue.pop(0)
        res.append(node.val)
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)

    return res

# Example usage
print(root.level_order_traversal(root))  # Output: [10, 5, 20, 3, 7, 15]
```

### **Conclusion**
Trees are fundamental data structures that are widely used in various applications, from representing hierarchical data to optimizing search and sort operations. Understanding binary trees and binary search trees is essential for solving complex problems efficiently. The operations of insertion, deletion, and traversal are crucial for manipulating and accessing data within trees.

---

Shall we move on to the next data structure, **Graphs**?
