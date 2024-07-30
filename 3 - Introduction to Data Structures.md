# Introduction to Data Structures

## What is a Data Structure?

- A data structure is a way of organizing and storing data.
- It is a collection of,
    - Data values
    - The relationships among them
    - The operations that can be applied to the structure.

## Abstract Data Types (ADT)

- Conceptual models of data structures that define,
    - The data values
    - The operations that can be applied to them
- They are independent of any particular implementation.
- Useful for understanding the properties of a data structure.
- Example: Stack, Queue, List, etc.

### ADT Specification

- Name of the ADT
- CRUD Operations
    - **Create**: Create a new instance of the data structure.
    - **Read**: Read the value of the data structure.
    - **Update**: Update the value of the data structure.
    - **Delete**: Delete the data structure.

## Array

- An array is a collection of homogeneous items stored at contiguous memory locations.
- **Contiguous Memory Locations**: Memory locations that are adjacent to each other.
- **Homogeneous Items**: Items of the same type.
- Each item can be accessed using an index.
- In c, a string is an array of char that is terminated by a null character. They are

### Types of Arrays

1. **One-Dimensional Array**: An array that stores data in a linear fashion.
2. **Multi-Dimensional Array**: An array that stores data in more than one dimensions.
3. **Dynamic Array**: An array that can grow or shrink in size (unlike a static array).

## Record

- A record is a collection of heterogeneous items stored at contiguous memory locations.
- **Heterogeneous Items**: Items of different types.
- Each item can be accessed using a field name/index.
- Also known as a `structure` or a `tuple`.

## Linked List

- A linked list is a collection of nodes where each node contains,
    - Data
    - A reference to the next node in the sequence.
- **Node**: A basic unit of a data structure.
- **Head**: The first node in the linked list.
- **Tail**: The last node in the linked list.

### Types of Linked Lists

1. **Singly Linked List**: Nodes contains a reference to the next node.
   ![Singly Linked List](./images/Linked%20List.png)
2. **Doubly Linked List**: Nodes contains a reference to the next and the previous node.
   ![Doubly Linked List](./images/Doubly%20linked%20List.png)
3. **Circular Linked List**: The last node points to the first node.
   ![Circular Linked List](./images/Circular%20linked%20list.png)

### Operations on Linked Lists

1. **Insert**: Insert a new node into the linked list.
2. **Search**: Search for a node in the linked list.
3. **Delete**: Delete a node from the linked list.

### Implementations of Linked Lists

- c language does not have built-in support for linked lists.
- Linked lists can be implemented using structures and pointers.
- C++, Python, Java use classes to implement linked lists.

## Queue

- A FIFO (First In First Out) data structure.
- **Enqueue**: Add an element to the end of the queue.
- **Dequeue**: Remove an element from the front of the queue.

### Priority Queue

- A queue where each element has a priority associated with it.
- Elements with higher priority are dequeued before elements with lower priority.
- Can be implemented using heaps.

## Stack

- A LIFO (Last In First Out) data structure.
- **Push**: Add an element to the top of the stack.
- **Pop**: Remove an element from the top of the stack.

## Dictionary

- Represents a set of key-value pairs.
