# Leetcode_Day45

# Day 45 – Search a 2D Matrix

## 📝 Problem
**LeetCode 74: Search a 2D Matrix**

Given an `m x n` integer matrix with the following properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given a target integer, return `true` if the target exists in the matrix. Otherwise, return `false`.

The solution must have a time complexity of `O(log(m * n))`.

## 💡 Approach: Binary Search

Instead of searching each row separately, treat the entire matrix as a **sorted 1D array**.

We use binary search with two pointers:
- `i = 0` → Starting index.
- `j = m * n - 1` → Ending index.

For every middle index:
1. Calculate the middle index.
2. Convert the 1D index into row and column coordinates:
   - `row = mid / n`
   - `col = mid % n`
3. Compare `matrix[row][col]` with the target.
4. If equal, return `true`.
5. If the current value is smaller, search the right half.
6. Otherwise, search the left half.

If the target is not found, return `false`.

## 💻 Java Solution

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;

        int i = 0;
        int j = (m * n) - 1;

        while (i <= j) {
            int mid = i + (j - i) / 2;

            int r = mid / n;
            int c = mid % n;

            if (matrix[r][c] == target) {
                return true;
            } else if (matrix[r][c] < target) {
                i = mid + 1;
            } else {
                j = mid - 1;
            }
        }

        return false;
    }
}
```

## ⏱️ Complexity Analysis

- **Time Complexity:** `O(log(m * n))`  
  Binary search eliminates half of the remaining elements in every iteration.

- **Space Complexity:** `O(1)`  
  Only a few variables are used, and no extra data structures are required.

## 📚 What I Learned

- How to apply binary search to a 2D matrix.
- How to represent a 2D matrix as a virtual 1D sorted array.
- How integer division and modulo help convert a 1D index into row and column coordinates.
- How choosing the right representation can make a problem much easier to solve.

## 🎯 Takeaway

Sometimes, the problem is not as difficult as it looks. Changing the way we look at the data can reveal a much simpler solution.
