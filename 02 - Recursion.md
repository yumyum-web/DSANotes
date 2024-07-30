# Recursion

## Introduction

- A function that either calls itself directly or indirectly is called a recursive function.
- Recursion is used when:
    - A problem can be divided into smaller problems that are similar to the original problem.
    - The solution of the original problem can be obtained by combining the solutions of the problems.
- Recursive functions must have a termination condition, called a base case.

## Recursion vs Iteration

| Recursion              | Iteration            |
|------------------------|----------------------|
| Easier to implement    | Harder to implement  |
| Slower due to overhead | Faster               |
| Uses more memory       | Uses less memory     |
| Can be more readable   | Can be less readable |

## Types of Recursion

1. **Direct Recursion:** A function calls itself.
2. **Indirect Recursion:** Function A makes a call to function B that results in calling the function A.
3. **Tail Recursion:** The recursive call is the last thing the function does.
4. **Non-tail Recursion:** The recursive call is not the last thing the function does.
5. **Multiple Recursion:** A function makes more than one recursive call.
6. **Nested Recursion:** A function is called within a recursive call.
7. **Mutual Recursion:** Two functions call each other.

## Divide and Conquer

- **Divide:** The problem is divided into smaller subproblems.
- **Conquer:** The subproblems are solved.
- **Combine:** The solutions of the subproblems are combined to solve the original problem.

- Examples:
    - Merge sort
    - Quick sort
    - Binary search

### Binary Search

- **Time complexity:** $O(\log n)$
- **Space complexity:** $O(1)$
- **Applications:** Used to search for an element in a sorted array.
- **Notes:**
    - More efficient than linear search.
    - The array must be sorted.
    - Not appropriate for linked lists.

#### Method

1. If the array is empty, return -1.
2. Calculate the middle index.
3. If the middle element is the target, return the index.
4. If the target is less than the middle element, search the left half.
5. If the target is greater than the middle element, search the right half.

<details>
<summary>C++ Implementation</summary>

```cpp
int binarySearch(int arr[], int target, int left, int right) {
    if (left > right) {
        return -1;
    }

    int mid = left + (right - left) / 2;

    if (arr[mid] == target) {
        return mid;
    } else if (target < arr[mid]) {
        return binarySearch(arr, target, left, mid - 1);
    } else {
        return binarySearch(arr, target, mid + 1, right);
    }
}
```

</details>

### pow Function in C

- **Time complexity:** $O(\log n)$
- **Space complexity:** $O(\log n)$
- **Applications:** Used to calculate the power of a number.

<details>
<summary>C Implementation</summary>

```cpp
/* Recursive function to calculate the power of a number */
int pow(int base, int exp) {
if (exp == 0) {
return 1;
}

int half = pow(base, exp / 2);

if (exp % 2 == 0) {
return half * half;
} else {
return base * half * half;
}
}
```

```cpp
/* Iterative function to calculate the power of a number */
int pow(int base, int exp) {
int result = 1;

while (exp > 0) {
if (exp % 2 == 1) {
result *= base;
}

base *= base;
exp /= 2;
}

return result;
}
```

</details>

## Solving Recurrence

1. **Substitution Method:** Guess the solution and then use mathematical induction to prove it.
2. **Recurrence Tree Method:** Draw a tree to represent the recursive calls.
3. **Master Theorem:** A formula for solving recurrence relations of the form $T(n) = aT(n/b) + f(n)$.

- Substitution method is too OP. Use master theorem if applicable.
- Recurrence tree method can be used to guess the solution and then prove it using the substitution method.

### Substitution Method

#### Method

1. Guess the form of the solution.
2. Use mathematical induction to find the constants and prove the solution.

#### Example

- **Recurrence relation:** $T(n) = 2T(n/2) + n$
- **Guess:** $T(n) = O(n\log n)$
- **Induction:**
    - **Base case:** $T(1) = 1 = O(1)$
    - **Inductive step:**
        - Assume $T(k) \leq ck\log k$ for $k < n$.
        - $T(n) = 2T(n/2) + n \leq 2(c(n/2)\log(n/2)) + n = cn\log n - cn\log 2 + n = cn\log n - cn + n$
        - $cn\log n - cn + n \leq cn\log n$ if $c \geq 1$
        - Therefore, $T(n) = O(n\log n)$

### Recurrence Tree Method

#### Method

1. Draw a tree to represent the recursive calls.
2. Calculate the cost of each level.
3. Sum the costs of all levels.
4. Find the height of the tree.
5. The total cost is the sum of the costs at each level multiplied by the number of levels.

#### Example

- **Recurrence relation:** $T(n) = 2T(n/2) + n$
- **Cost:** $n$ at each level
- **Height:** $\log n$
- **Total cost:** $n\log n$
- **Time complexity:** $O(n\log n)$

### Master Theorem

#### Method

- Most useful for divide and conquer algorithms.
- **Recurrence relation:** $T(n) = aT(n/b) + f(n)$
- **Constants:**
    - $a$: Number of subproblems.
    - $b$: Factor by which the input size is reduced.
    - $f(n)$: Cost of dividing the problem and combining the solutions.

1. $ If\ n^{\log_b a} > f(n),\ then\ T(n) = \Theta(n^{\log_b a}) $
    - The work to split/combine a problem is negligible compared to subproblems.
    - **Example:** Binary search
2. $ If\ n^{\log_b a} = f(n),\ then\ T(n) = \Theta(n^{\log_b a}\log n) $
    - The work to split/combine a problem is comparable to subproblems.
    - **Example:** Merge sort
3. $ If\ n^{\log_b a} < f(n),\ then\ T(n) = \Theta(f(n)) $
    - The work to split/combine a problem is dominant compared to subproblems.
    - **Example:** Fibonacci sequence

#### Example

- **Recurrence relation:** $T(n) = 2T(n/2) + n$
- $a = 2$, $b = 2$, $f(n) = n$
- $\log_b a = \log_2 2 = 1$
- $n^{\log_b a} = n$
- $f(n) = \Theta(n) = n^{\log_b a}$
- **Case 2 applies:** $T(n) = \Theta(n\log n)$
- **Time complexity:** $O(n\log n)$
