# Algorithm  Design Techniques

## Why design algorithms?

- Used to find solutions to problems

## Types of solutions

- **Optimal solution**: The best solution to a problem
- **Good enough solution**: A solution that is good enough to solve the problem
    - _Good enough_ is defined by a set of parameters
- **Partial solution**: A solution that solves part of the problem
    - It Can be extended to solve the whole problem
- **Feasible solution**: A solution that satisfies the constraints of the problem

## Traits of problems

### Overlapping subproblems

- **Definition**: A problem has overlapping subproblems if it can be broken down into smaller subproblems that are
  reused multiple times.
- **Example**: Fibonacci series
- **Solution**:
    - Dynamic programming

### Optimal substructure

- **Definition**: A problem has optimal substructure if an optimal solution can be constructed from optimal solutions
  of its subproblems.
- **Example**: Shortest path problem
- **Solution**:
    - Dynamic programming
    - Greedy algorithms

### Greedy choice property

- **Definition**: A problem has the greedy choice property if a globally optimal solution can be reached by making a
  locally optimal choice.
- **Example**: Fractional knapsack problem
- **Solution**:
    - Greedy algorithms

## Algorithm types

### Brute force

- **Approach**: A method of solving problems by trying all possible solutions.
- **Advantages**:
    - Can identify multiple solutions.
- **Disadvantages**:
    - Time-consuming
    - Inefficient
    - Not suitable for large problems

### Divide and conquer

- **Approach**: A method of solving problems by dividing them into smaller subproblems and solving each subproblem
  independently.
- Mostly implemented using recursion.
- **Advantages**:
    - Easier to implement
    - Can be parallelized
- **Disadvantages**:
    - Overhead of recursion
    - Extra space required for recursion
    - Same subproblems may be solved multiple times

### Dynamic programming

- **Approach**: A method of solving problems by breaking them down into simpler subproblems and solving each subproblem
  only once.
- Usually is an optimization over divide and conquer.
- Used when the subproblems are overlapping.
- **Disadvantages**:
    - Requires extra space for storing the results of the subproblems
    - It May not be suitable for large problems

#### Types of dynamic programming

- **Top-down**:
    - Starts from the top and solves the subproblems in a recursive manner.
    - Uses memoization to store the results of the subproblems.
    - **Memoization**: Storing the results of the subproblems by caching them.
- **Bottom-up**:
    - Starts from the bottom and solves the subproblems iteratively.
    - Uses tabulation to store the results of the subproblems.

### Greedy algorithms

- **Approach**: A method of solving problems by making the best choice at each step.
- **Advantages**:
    - Has a lower time complexity
    - Suitable for large problems
- **Disadvantages**:
    - Getting the optimal solution depends on the accuracy of the greedy choice
    - May not work for all problems

