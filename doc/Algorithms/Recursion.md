### **Recursion in Python**

#### **Description**
Recursion is a programming technique where a function calls itself to solve smaller instances of the same problem until it reaches a base case. The recursive approach can be very elegant and is often used to solve problems that can naturally be divided into smaller subproblems. However, recursion must be used carefully to avoid infinite loops and excessive memory use.

#### **Key Concepts in Recursion**
- **Base Case**: The condition under which the recursive function stops calling itself. Without a base case, recursion would continue indefinitely, leading to a stack overflow.
- **Recursive Case**: The part of the function that includes the recursive call, which moves the problem towards the base case.

### **Examples of Recursion**

### **1. Factorial Calculation**

The factorial of a non-negative integer \( n \) is the product of all positive integers less than or equal to \( n \). It is denoted as \( n! \). For example, \( 5! = 5 \times 4 \times 3 \times 2 \times 1 = 120 \).

#### **Recursive Formula**:
\[
n! = \begin{cases} 
1 & \text{if } n = 0 \\
n \times (n-1)! & \text{if } n > 0 
\end{cases}
\]

#### **Python Implementation**:

```python
def factorial(n):
    if n == 0 or n == 1:  # Base case
        return 1
    else:
        return n * factorial(n - 1)  # Recursive case

# Example usage
print(factorial(5))  # Output: 120
```

**Explanation**:
- When \( n \) reaches 0 or 1, the function returns 1 (the base case).
- For other values of \( n \), the function calls itself with \( n-1 \) and multiplies the result by \( n \).

**Time Complexity**: \( O(n) \)

**Space Complexity**: \( O(n) \) (due to the call stack)

### **2. Tower of Hanoi**

The Tower of Hanoi is a classic recursive problem involving three rods and a number of disks of different sizes. The objective is to move the entire stack of disks from the source rod to the destination rod, following these rules:
1. Only one disk can be moved at a time.
2. A disk can only be placed on top of a larger disk.
3. All disks must be moved from the source to the destination rod using an auxiliary rod.

#### **Recursive Solution**:
- Move the top \( n-1 \) disks from the source rod to the auxiliary rod.
- Move the nth (largest) disk directly to the destination rod.
- Move the \( n-1 \) disks from the auxiliary rod to the destination rod.

#### **Python Implementation**:

```python
def tower_of_hanoi(n, source, destination, auxiliary):
    if n == 1:
        print(f"Move disk 1 from {source} to {destination}")
        return
    tower_of_hanoi(n-1, source, auxiliary, destination)
    print(f"Move disk {n} from {source} to {destination}")
    tower_of_hanoi(n-1, auxiliary, destination, source)

# Example usage
tower_of_hanoi(3, 'A', 'C', 'B')
```

**Explanation**:
- The function is called recursively to move \( n-1 \) disks to the auxiliary rod, then moves the nth disk to the destination rod, and finally moves the \( n-1 \) disks from the auxiliary rod to the destination rod.
- This process repeats until all disks are moved to the destination rod.

**Time Complexity**: \( O(2^n - 1) \) (exponential)

**Space Complexity**: \( O(n) \) (due to the call stack)

### **Comparison of Recursion Examples**

| Problem            | Base Case                  | Recursive Case                                                | Time Complexity | Space Complexity |
|--------------------|----------------------------|----------------------------------------------------------------|-----------------|------------------|
| **Factorial**      | \( n = 0 \) or \( n = 1 \) | Multiply \( n \) by the factorial of \( n-1 \)                 | \( O(n) \)      | \( O(n) \)       |
| **Tower of Hanoi** | \( n = 1 \)                | Move \( n-1 \) disks to auxiliary, move nth disk, then move \( n-1 \) disks | \( O(2^n) \)    | \( O(n) \)       |

### **Conclusion**
Recursion is a powerful tool in problem-solving, particularly for problems that naturally fit a divide-and-conquer approach. However, recursion can also be inefficient if not carefully managed, particularly in terms of space complexity, due to the call stack. Understanding both the power and the limitations of recursion is key to effectively applying it in programming.
