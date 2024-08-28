### **Linked Lists in Python**

#### **Description**
A linked list is a data structure consisting of a sequence of nodes where each node contains data and a reference (or pointer) to the next node in the sequence. Unlike arrays or lists, linked lists do not store their elements in contiguous memory locations. This structure allows for efficient insertion and deletion of elements without the need for shifting elements, as is the case with arrays.

#### **Types of Linked Lists**

##### **Singly Linked List**
- **Description**: In a singly linked list, each node contains a reference to the next node in the sequence. The last node points to `None`, indicating the end of the list.

##### **Doubly Linked List**
- **Description**: In a doubly linked list, each node contains two references: one to the next node and another to the previous node. This allows for traversal in both directions.

### **Basic Linked List Operations**

To better understand linked lists, we'll implement a simple singly linked list in Python. Each node in the linked list will be represented by a `Node` class, and the linked list itself will be managed by a `LinkedList` class.

#### **Node Class**
The `Node` class represents each element in the linked list.

```python
class Node:
    def __init__(self, data):
        self.data = data  # The data value
        self.next = None  # The reference to the next node
```

#### **Singly Linked List Implementation**
Here's how you might implement the basic operations for a singly linked list:

##### **Traversal**
Traversal involves visiting each node starting from the head.

```python
class LinkedList:
    def __init__(self):
        self.head = None  # Initialize the head of the list as None

    def traverse(self):
        current_node = self.head
        while current_node:
            print(current_node.data, end=" -> ")
            current_node = current_node.next
        print("None")

# Example usage
linked_list = LinkedList()
linked_list.head = Node(1)
second_node = Node(2)
third_node = Node(3)

linked_list.head.next = second_node  # Link first node to second
second_node.next = third_node        # Link second node to third

linked_list.traverse()  # Output: 1 -> 2 -> 3 -> None
```

##### **Insertion**
There are several ways to insert a new node into a linked list: at the beginning, at the end, or after a given node.

- **Insert at the Beginning**:

```python
def insert_at_beginning(self, new_data):
    new_node = Node(new_data)
    new_node.next = self.head
    self.head = new_node

# Example usage
linked_list.insert_at_beginning(0)
linked_list.traverse()  # Output: 0 -> 1 -> 2 -> 3 -> None
```

- **Insert at the End**:

```python
def insert_at_end(self, new_data):
    new_node = Node(new_data)
    if self.head is None:
        self.head = new_node
        return
    last_node = self.head
    while last_node.next:
        last_node = last_node.next
    last_node.next = new_node

# Example usage
linked_list.insert_at_end(4)
linked_list.traverse()  # Output: 0 -> 1 -> 2 -> 3 -> 4 -> None
```

- **Insert After a Specific Node**:

```python
def insert_after_node(self, prev_node, new_data):
    if not prev_node:
        print("Previous node is not in the list")
        return
    new_node = Node(new_data)
    new_node.next = prev_node.next
    prev_node.next = new_node

# Example usage
linked_list.insert_after_node(linked_list.head.next, 1.5)
linked_list.traverse()  # Output: 0 -> 1 -> 1.5 -> 2 -> 3 -> 4 -> None
```

##### **Deletion**
Deleting a node from a linked list can be done in different ways: by value, by position, or at the beginning/end.

- **Delete by Value**:

```python
def delete_node(self, key):
    temp = self.head

    # If the head node itself holds the key
    if temp is not None:
        if temp.data == key:
            self.head = temp.next
            temp = None
            return

    # Search for the key to be deleted
    prev = None
    while temp is not None:
        if temp.data == key:
            break
        prev = temp
        temp = temp.next

    # If the key was not present in the linked list
    if temp == None:
        return

    # Unlink the node from the linked list
    prev.next = temp.next
    temp = None

# Example usage
linked_list.delete_node(1.5)
linked_list.traverse()  # Output: 0 -> 1 -> 2 -> 3 -> 4 -> None
```

- **Delete by Position**:

```python
def delete_node_at_position(self, position):
    if self.head is None:
        return

    temp = self.head

    if position == 0:
        self.head = temp.next
        temp = None
        return

    for i in range(position - 1):
        temp = temp.next
        if temp is None:
            break

    if temp is None:
        return
    if temp.next is None:
        return

    next_node = temp.next.next
    temp.next = None
    temp.next = next_node

# Example usage
linked_list.delete_node_at_position(3)
linked_list.traverse()  # Output: 0 -> 1 -> 2 -> 4 -> None
```

#### **Doubly Linked List**
A doubly linked list allows traversal in both directions by having each node contain references to both the next and the previous node.

Here’s a basic structure of a `DoublyLinkedList` class:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None  # Reference to the previous node

class DoublyLinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
            return
        last = self.head
        while last.next:
            last = last.next
        last.next = new_node
        new_node.prev = last

    def traverse_forward(self):
        node = self.head
        while node:
            print(node.data, end=" -> ")
            node = node.next
        print("None")

    def traverse_backward(self):
        node = self.head
        while node.next:
            node = node.next
        while node:
            print(node.data, end=" -> ")
            node = node.prev
        print("None")

# Example usage
dll = DoublyLinkedList()
dll.append(1)
dll.append(2)
dll.append(3)

dll.traverse_forward()  # Output: 1 -> 2 -> 3 -> None
dll.traverse_backward() # Output: 3 -> 2 -> 1 -> None
```

### **Conclusion**
Linked lists are versatile data structures that are fundamental to many algorithms and systems. They provide efficient ways to insert and delete elements without the need for shifting, as in arrays. Understanding both singly and doubly linked lists allows you to choose the right type for your application based on the needs for forward and backward traversal, insertion, and deletion.
