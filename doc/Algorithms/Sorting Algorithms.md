### **Sorting Algorithms in Python**

Sorting algorithms are fundamental to computer science, and they are used to arrange data in a specific order (usually ascending or descending). Understanding different sorting algorithms helps in selecting the most appropriate one for a given problem based on its characteristics and constraints. Here are three commonly used sorting algorithms: Bubble Sort, Merge Sort, and Quick Sort.

---

### **Bubble Sort**

#### **Description**
Bubble Sort is a simple comparison-based sorting algorithm. It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

#### **Steps**:
1. Start at the beginning of the list.
2. Compare the first two elements.
3. If the first is greater than the second, swap them.
4. Move to the next pair and repeat the process until the end of the list.
5. Repeat the entire process until no swaps are needed (the list is sorted).

#### **Python Implementation**:

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        # Flag to check if any swapping happened
        swapped = False
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                # Swap if the element found is greater than the next element
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True
        # If no swapping happened in the inner loop, the array is sorted
        if not swapped:
            break

# Example usage
arr = [64, 34, 25, 12, 22, 11, 90]
bubble_sort(arr)
print("Sorted array:", arr)  # Output: Sorted array: [11, 12, 22, 25, 34, 64, 90]
```

#### **Time Complexity**: O(n²)
- **Best Case**: O(n) (when the array is already sorted)
- **Worst Case**: O(n²)

**Space Complexity**: O(1)

**Pros**: Simple to understand and implement.
**Cons**: Inefficient for large datasets.

---

### **Merge Sort**

#### **Description**
Merge Sort is a divide-and-conquer algorithm. It divides the list into two halves, recursively sorts each half, and then merges the two sorted halves back together. It is known for its efficiency and stability.

#### **Steps**:
1. Divide the list into two halves.
2. Recursively sort each half.
3. Merge the two sorted halves into one sorted list.

#### **Python Implementation**:

```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2  # Finding the mid of the array
        left_half = arr[:mid]  # Dividing the elements into 2 halves
        right_half = arr[mid:]

        merge_sort(left_half)  # Sorting the first half
        merge_sort(right_half)  # Sorting the second half

        i = j = k = 0

        # Copy data to temp arrays L[] and R[]
        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        # Checking if any element was left
        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1

# Example usage
arr = [38, 27, 43, 3, 9, 82, 10]
merge_sort(arr)
print("Sorted array:", arr)  # Output: Sorted array: [3, 9, 10, 27, 38, 43, 82]
```

#### **Time Complexity**: O(n log n)
- **Best Case**: O(n log n)
- **Worst Case**: O(n log n)

**Space Complexity**: O(n)

**Pros**: Stable, efficient for large datasets, and guarantees O(n log n) time complexity.
**Cons**: Requires additional space proportional to the size of the array.

---

### **Quick Sort**

#### **Description**
Quick Sort is another divide-and-conquer algorithm. It works by selecting a 'pivot' element and partitioning the array around the pivot. The elements less than the pivot are placed on the left, and those greater are on the right. The process is then repeated recursively for the left and right subarrays.

#### **Steps**:
1. Pick a pivot element (various methods exist, such as picking the first element, the last element, or a random element).
2. Partition the array such that elements less than the pivot are on the left, and those greater than the pivot are on the right.
3. Recursively apply the same logic to the left and right subarrays.

#### **Python Implementation**:

```python
def partition(arr, low, high):
    i = low - 1  # Index of smaller element
    pivot = arr[high]  # Pivot element is the last element

    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]  # Swap

    arr[i + 1], arr[high] = arr[high], arr[i + 1]  # Swap the pivot element with the element at i + 1
    return i + 1

def quick_sort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)  # Partitioning index

        quick_sort(arr, low, pi - 1)  # Sort the elements on the left of pivot
        quick_sort(arr, pi + 1, high)  # Sort the elements on the right of pivot

# Example usage
arr = [10, 7, 8, 9, 1, 5]
quick_sort(arr, 0, len(arr) - 1)
print("Sorted array:", arr)  # Output: Sorted array: [1, 5, 7, 8, 9, 10]
```

#### **Time Complexity**: O(n log n) on average
- **Best Case**: O(n log n)
- **Worst Case**: O(n²) (when the smallest or largest element is always picked as the pivot, leading to unbalanced partitions)

**Space Complexity**: O(log n)

**Pros**: Faster than Merge Sort in practice for most inputs, requires less additional space.
**Cons**: Worst-case time complexity is O(n²), but this is rare with good pivot selection.

---

### **Comparison Summary**

| Algorithm    | Time Complexity (Best) | Time Complexity (Average) | Time Complexity (Worst) | Space Complexity | Stability | Use Case               |
|--------------|------------------------|---------------------------|-------------------------|------------------|-----------|------------------------|
| **Bubble Sort** | O(n)                    | O(n²)                      | O(n²)                    | O(1)             | Stable    | Small datasets, educational purposes |
| **Merge Sort**  | O(n log n)              | O(n log n)                 | O(n log n)               | O(n)             | Stable    | Large datasets, when stability is important |
| **Quick Sort**  | O(n log n)              | O(n log n)                 | O(n²)                    | O(log n)         | Unstable  | Large datasets, when space is a concern |

### **Conclusion**
Understanding these three sorting algorithms provides a solid foundation for choosing the right sorting technique based on the specific needs of your problem. Bubble Sort is simple but inefficient for large datasets, Merge Sort is stable and consistently O(n log n) but requires additional space, and Quick Sort is often faster in practice but has the potential for a worst-case scenario if not implemented carefully.
