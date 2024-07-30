# Heap

- Heap is a complete binary tree that satisfies the heap property.
- There are two types of heap:
    - Max heap: In which the value of parent node is greater than or equal to the value of child node.
    - Min heap: In which the value of parent node is less than or equal to the value of child node.

### Representation

- Heap is commonly represented using array.
    - Index starts from 1.
    - For a node at index `i`:
        - Left child: `2*i`
        - Right child: `2*i + 1`
        - Parent: `i/2`
- Can also be as a binary tree.

### HeapSort related operations:

#### Heapify

- Makes a subtree satisfy the heap property.
- Can only be applied to a node that has two heapified child trees.
- Steps for a _max heap:_
    1. For a node at index `i`, find the largest element among the node and its children.
    2. If the largest element is not the node itself, swap the node with the largest element and recursively heapify
       that subtree.
- Time complexity: $O(\log n)$
- This `n` is th number of nodes in the subtree rooted at the given node.

```cpp
void heapify(int arr[], int n, int i) {
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;

    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }

    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }

    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}
```

#### Build Heap

- Converts an array into a heap.
- Start from the last non-leaf node and heapify all nodes in reverse level order.
- Time complexity: $O(n)$

```cpp
void buildHeap(int arr[], int n) {
    for (int i = n/2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
}
```

#### Heap Sort

- Sorts an array using heap data structure.
- Steps for sorting in _ascending order:_
    1. Build a max heap from the array.
    2. Swap the root element with the last element and heapify the reduced heap.
    3. Repeat step 2 for all elements.
- Time complexity: $O(n\log n)$
- Space complexity: $O(1)$
- Stable: No
- In-place: Yes

```cpp
void heapSort(int arr[], int n) {
    buildHeap(arr, n);

    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}
```

### Priority Queue Related Operations

- Priority queue is an abstract data type.
- It is a queue where each element has a priority associated with it.
- Elements are dequeued based on their priority.
- Can be implemented using heaps.

| Operation       | Description                                                    | Time Complexity |
|-----------------|----------------------------------------------------------------|:---------------:|
| Insert          | Insert an element into the queue                               |   $O(\log n)$   |
| Peek            | Get the element with the highest/lowest priority               |     $O(1)$      |
| Extract         | Remove and return the element with the highest/lowest priority |   $O(\log n)$   |
| Change Priority | Change the priority of an element                              |   $O(\log n)$   |
