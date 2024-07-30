# Complexity Analysis

## Introduction

- Complexity analysis is the process of determining how efficient an algorithm is.
- It is a way to measure how an algorithm responds to an increase in the size of the input data.
- There are two types of complexity analysis:
    - Time complexity
    - Space complexity
- **Asymptotic analysis:** analyzing the behavior of a function as the input size approaches infinity. Written using
  asymptotic notation.
- Three cases of time complexity:
    - Best case (Big Omega)
    - Average case (Big Theta)
    - Worst case (Big O)

## Asymptotic Notations

| Notation | Name         | Basic Relation                              | Crude Definition                         | Example                  |
|----------|--------------|---------------------------------------------|------------------------------------------|--------------------------|
| o        | Little o     | $f(n)$ grows **slower** than $g(n)$         | $f(n) < c\cdot g(n)$                     | $2n^2 + 3n + 1 = o(n^3)$ |
| O        | Big O        | $f(n)$ grows **no faster** than $g(n)$      | $f(n) <= c\cdot g(n)$                    | $2n^2 + 3n + 1 = O(n^2)$ |
| Θ        | Theta        | $f(n)$ grows at the **same rate** as $g(n)$ | $c_1\cdot g(n) <= f(n) <= c_2\cdot g(n)$ | $2n^2 + 3n + 1 = Θ(n^2)$ |
| ω        | Little omega | $f(n)$ grows **faster** than $g(n)$         | $f(n) > c\cdot g(n)$                     | $2n^2 + 3n + 1 = ω(n)$   |
| Ω        | Big Omega    | $f(n)$ grows **no slower** than $g(n)$      | $f(n) >= c\cdot g(n)$                    | $2n^2 + 3n + 1 = Ω(n)$   |

_**Note:** The above table is a generalization. The actual definitions are more complex._

- When choosing a $g(n)$:
    - Choose the tightest function.
    - Choose the simplest function.
- Big O notation is the most commonly used notation.

## Complexity theory

- **Time complexity:** The amount of time an algorithm takes in terms of the input size.
- **Space complexity:** The amount of memory an algorithm uses in terms of the input size.
- **Complexity classes:** A set of problems that can be solved by algorithms with a certain time or space complexity.
- **P:** The set of problems that can be solved in polynomial time.
- **NP:** The set of problems that can be verified in polynomial time.
- **NP-complete:** The hardest problems in NP.
- **NP-hard:** At least as hard as the hardest problems in NP.
- **P vs NP problem:** Whether every problem in NP is also in P.
- **Exponential time:** An algorithm that takes $O(2^n)$ time.
- **Factorial time:** An algorithm that takes $O(n!)$ time.
- **Logarithmic time:** An algorithm that takes $O(\log n)$ time.
- **Linear time:** An algorithm that takes $O(n)$ time.
- **Quadratic time:** An algorithm that takes $O(n^2)$ time.
- **Cubic time:** An algorithm that takes $O(n^3)$ time.
- **Polynomial time:** An algorithm that takes $O(n^k)$ time.

## Comparison of Time Complexities

constant < logarithmic < linear < linearithmic < polynomial < exponential < factorial

$O(1) < O(\log n) < O(n) < O(n\log n) < O(n^k) < O(k^n) < O(n!)$

## Sorting Algorithms

### Bubble Sort

- **Time complexity:**
    - Best case: $O(n)$
    - Average case: $O(n^2)$
    - Worst case: $O(n^2)$
- **Space complexity:** $O(1)$
- **Stable:** Yes
- **In-place:** Yes
- **Method:** Repeatedly swap the adjacent elements if they are in the wrong order.
- **Optimized version:** Flag to check if any swap is made in the inner loop. If not, the array is already sorted.
- **Applications:** Used when the input is almost sorted.
- **Notes:**
    - Not suitable for large datasets.
    - Not suitable for datasets with a large range of values.

### Selection Sort

- **Time complexity:**
    - Best case: $O(n^2)$
    - Average case: $O(n^2)$
    - Worst case: $O(n^2)$
- **Space complexity:** $O(1)$
- **Stable:** No
- **In-place:** Yes
- **Method:** Select the minimum element from the unsorted portion and swap it with the first element.
- **Applications:** Used when memory writes are a concern.
- **Notes:**
    - Not suitable for large datasets.
    - Not suitable for datasets with a large range of values.

### Insertion Sort

- **Time complexity:**
    - Best case: $O(n)$
    - Average case: $O(n^2)$
    - Worst case: $O(n^2)$
- **Space complexity:** $O(1)$
- **Stable:** Yes
- **In-place:** Yes
- **Method:** Build the sorted array one element at a time by inserting the unsorted element in its correct position.
- **Applications:** Used when the dataset is small or almost sorted.
- **Notes:**
    - Efficient for small datasets.
    - Efficient for datasets that are _nearly sorted._
    - More efficient in practice than other $O(n^2)$ algorithms.

### Merge Sort

- **Time complexity:**
    - Best case: $O(n\log n)$
    - Average case: $O(n\log n)$
    - Worst case: $O(n\log n)$
- **Space complexity:** $O(n)$
- **Stable:** Yes
- **In-place:** No
- **Method:** Divide the array into two halves, sort the halves, and merge them.
- **Applications:** Used when a stable sort is required.
- **Notes:**
    - Efficient for large datasets.
    - Slower compared to other $O(n\log n)$ algorithms.
    - Used in external sorting.
    - Used in sorting linked lists.

#### Method

1. If the array has one element, it is already sorted.
2. Divide the array into two halves.
3. Recursively sort the two halves.
4. Merge the sorted halves.
    1. Create an auxiliary array.
    2. Compare the first element of the two halves and add the smaller one to the auxiliary array.
    3. Repeat until one half is empty.
    4. Add the remaining elements to the auxiliary array.

<details>
<summary>C++ Implementation</summary>

```cpp
int[] merge(int left[], int right[]) {
    int result[] = new int[left.length + right.length];
    int i = 0, j = 0, k = 0;

    while (i < left.length && j < right.length) {
        if (left[i] <= right[j]) { // Use <= to keep it stable.
            result[k++] = left[i++];
        } else {
            result[k++] = right[j++];
        }
    }

    while (i < left.length) { 
        result[k++] = left[i++];
    }

    while (j < right.length) {
        result[k++] = right[j++];
    }

    return result;
}

int[] mergeSort(int arr[]) {
    if (arr.length <= 1) {
        return arr;
    }

    int mid = arr.length / 2;
    int left[] = mergeSort(Arrays.copyOfRange(arr, 0, mid));
    int right[] = mergeSort(Arrays.copyOfRange(arr, mid, arr.length));

    return merge(left, right);
}
```

</details>

### Quick Sort

- **Time complexity:**
    - Best case: $O(n\log n)$
    - Average case: $O(n\log n)$
    - Worst case: $O(n^2)$
    - Worst case can be avoided by using a random pivot.
- **Space complexity:** $O(\log n)$
- **Stable:** No
- **In-place:** Yes
- **Method:** Choose a pivot, partition the array such that elements smaller than the pivot are on the left and elements
  greater than the pivot are on the right, and recursively sort the sub-arrays.
- **Applications:** Used when average time complexity is important.
- **Notes:**
    - Efficient for large datasets.
    - Not suitable for datasets with a large range of values.
    - Used in the C library function `qsort`.

### Heap Sort

- **Time complexity:**
    - Best case: $O(n\log n)$
    - Average case: $O(n\log n)$
    - Worst case: $O(n\log n)$
    - Worst case is guaranteed.
- **Space complexity:** $O(1)$
- **Stable:** No
- **In-place:** Yes
- **Method:** Build a max heap, swap the root with the last element, and heapify the reduced heap.
- **Applications:** Used when a guaranteed worst-case time complexity is required.
- **Notes:**
    - Efficient for large datasets.
    - Not suitable for datasets with a large range of values.
    - Used in the C++ standard library function `std::make_heap`.

## Tips

- **Nested logic:** Use proper branching of logic to reduce unnecessary checks. Instead of separate if-else blocks, use
  nested if-else blocks/else-if ladder.
- **Loop optimization:** Use the correct loop for the task. For example, use a `for` loop when the number of iterations
  is
  known. Use a `while` loop when the number of iterations is unknown.
- **Iterative vs. recursive:** Use an iterative approach when the recursive approach is inefficient due to stack space
  usage.
