# 643. Maximum Average Subarray I

## Problem Statement
Given an integer array `nums` consisting of `n` elements and an integer `k`, return the maximum average value of a subarray of length `k` rounded down to the nearest integer.

## Example
```plaintext
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12

Explanation: Maximum average is (12,-5,-6,50)/4 = 12.75, which is rounded down to 12.
```

## Explanation
1. We need to find the maximum average of any contiguous subarray of length `k` in the given array `nums`.
2. We can calculate the sum of the first `k` elements, then use a sliding window technique to find the sum of the next subarrays by subtracting the first element of the previous window and adding the next element of the current window.
3. The maximum sum found in these calculations is then divided by `k` to find the average.
4. Finally, we return the maximum average as an integer by rounding down.

## Implementation
Here is a sample implementation in Python:

```python
def findMaxAverage(nums, k):
    max_sum = sum(nums[:k])
    current_sum = max_sum
    for i in range(k, len(nums)):
        current_sum += nums[i] - nums[i - k]
        max_sum = max(max_sum, current_sum)
    return max_sum // k
```

## Complexity Analysis
- **Time Complexity**: O(n), where `n` is the number of elements in `nums`. We traverse the array once.
- **Space Complexity**: O(1), we use a constant amount of space for variables.
