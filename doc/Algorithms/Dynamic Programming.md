### **Dynamic Programming in Python**

#### **Description**
Dynamic Programming (DP) is a method for solving complex problems by breaking them down into simpler subproblems, solving each of these subproblems just once, and storing their solutions – typically in a table or array – to avoid the need to recompute these solutions. This approach is particularly effective for optimization problems where the same subproblems are solved multiple times, such as in recursive algorithms.

Dynamic Programming is characterized by two main strategies:
- **Overlapping Subproblems**: The problem can be broken down into smaller, simpler subproblems, and these subproblems are solved multiple times.
- **Optimal Substructure**: The optimal solution to the problem can be constructed from the optimal solutions of its subproblems.

#### **Examples of Dynamic Programming**

### **1. Fibonacci Sequence**

The Fibonacci sequence is a classic example used to illustrate dynamic programming. The sequence is defined as:
\[ F(n) = F(n-1) + F(n-2) \]
with base cases:
\[ F(0) = 0, \, F(1) = 1 \]

Using dynamic programming, we can compute Fibonacci numbers efficiently by storing the results of previous computations.

##### **Naive Recursive Approach (Inefficient)**

```python
def fib_recursive(n):
    if n <= 1:
        return n
    return fib_recursive(n-1) + fib_recursive(n-2)

# Example usage
print(fib_recursive(10))  # Output: 55
```

**Problem**: This naive approach is highly inefficient because it recomputes the same Fibonacci values multiple times, leading to an exponential time complexity \( O(2^n) \).

##### **Efficient Approach Using Memoization**

Memoization stores the results of expensive function calls and returns the cached result when the same inputs occur again.

```python
def fib_memoization(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_memoization(n-1, memo) + fib_memoization(n-2, memo)
    return memo[n]

# Example usage
print(fib_memoization(10))  # Output: 55
```

**Time Complexity**: \( O(n) \)

**Space Complexity**: \( O(n) \)

##### **Tabulation Approach**

The tabulation approach involves filling up a table (an array) iteratively to solve the problem.

```python
def fib_tabulation(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

# Example usage
print(fib_tabulation(10))  # Output: 55
```

**Time Complexity**: \( O(n) \)

**Space Complexity**: \( O(n) \)

### **2. Knapsack Problem**

The Knapsack Problem is a classic optimization problem. Given a set of items, each with a weight and a value, the goal is to determine the maximum value that can be obtained by selecting a subset of the items such that their total weight does not exceed a given limit (the knapsack’s capacity).

#### **Problem Statement**
Given weights `w = [w1, w2, ..., wn]`, values `v = [v1, v2, ..., vn]`, and a knapsack capacity `W`, find the maximum value that can be carried in the knapsack.

##### **Dynamic Programming Approach**

The idea is to build a DP table where `dp[i][j]` represents the maximum value that can be obtained using the first `i` items with a capacity of `j`.

- If the weight of the item is greater than the capacity, skip the item.
- Otherwise, the value is the maximum of either including the item or excluding it.

```python
def knapsack(weights, values, capacity):
    n = len(values)
    dp = [[0 for _ in range(capacity + 1)] for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(1, capacity + 1):
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w], dp[i-1][w - weights[i-1]] + values[i-1])
            else:
                dp[i][w] = dp[i-1][w]

    return dp[n][capacity]

# Example usage
weights = [1, 2, 3, 4]
values = [10, 20, 30, 40]
capacity = 6
print(knapsack(weights, values, capacity))  # Output: 60
```

**Explanation**:
- **Base Case**: If there are no items or the capacity is 0, the maximum value is 0.
- **DP Relation**: The maximum value is either obtained by including the current item (and adding its value) or by excluding it.

**Time Complexity**: \( O(n \times W) \), where `n` is the number of items and `W` is the knapsack capacity.

**Space Complexity**: \( O(n \times W) \)

### **Comparison of Techniques**

| Technique    | Description | Time Complexity | Space Complexity | Use Case Example                  |
|--------------|-------------|-----------------|------------------|-----------------------------------|
| **Memoization** | Top-down approach storing subproblem results in a hash map or array | \( O(n) \) | \( O(n) \) | Fibonacci sequence              |
| **Tabulation**  | Bottom-up approach filling a table iteratively | \( O(n) \) | \( O(n) \) | Fibonacci sequence, Knapsack problem |

### **Conclusion**
Dynamic Programming is a powerful technique that can solve complex problems efficiently by breaking them down into simpler subproblems and storing the results of these subproblems to avoid redundant calculations. Whether through memoization or tabulation, DP can drastically reduce the time complexity of recursive solutions and is essential for tackling optimization problems.
