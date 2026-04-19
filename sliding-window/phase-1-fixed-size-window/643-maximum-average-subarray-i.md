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


# Maximum Average Subarray I — Full Explanation

## Problem

You are given an integer array `nums` and an integer `k`.

Find a contiguous subarray of length exactly `k` that has the **maximum average value**, and return that average.

---

## Example

### Input

```python
nums = [1, 12, -5, -6, 50, 3]
k = 4
```

### Output

```python
12.75
```

### Why?

The subarray with the maximum average is:

```python
[12, -5, -6, 50]
```

Its sum is:

```python
12 + (-5) + (-6) + 50 = 51
```

Its average is:

```python
51 / 4 = 12.75
```

---

## Key Idea: Fixed-Size Sliding Window

Because the subarray length must be **exactly `k`**, this is a **fixed-size sliding window** problem.

Instead of calculating the sum of every subarray from scratch, we:

1. Compute the sum of the first window of size `k`
2. Slide the window one step to the right
3. Add the new element entering the window
4. Remove the old element leaving the window
5. Keep track of the maximum sum seen

At the end, return:

```python
max_sum / k
```

---

## Brute Force Approach

A brute force way would be:

- Try every subarray of length `k`
- Compute its sum
- Keep the maximum

### Brute force code

```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        max_avg = float("-inf")

        for i in range(len(nums) - k + 1):
            curr_sum = sum(nums[i:i+k])
            max_avg = max(max_avg, curr_sum / k)

        return max_avg
```

### Time Complexity

- There are about `n` windows
- Each `sum(nums[i:i+k])` takes `O(k)`

So total time is:

```python
O(n * k)
```

This is slower than needed.

---

## Optimized Sliding Window Approach

### Code

```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        window_sum = sum(nums[:k])
        max_sum = window_sum

        for right in range(k, len(nums)):
            window_sum += nums[right] - nums[right - k]
            max_sum = max(max_sum, window_sum)

        return max_sum / k
```

---

## How This Works

### Step 1: Compute the first window sum

If:

```python
nums = [1, 12, -5, -6, 50, 3]
k = 4
```

Then the first window is:

```python
[1, 12, -5, -6]
```

Its sum is:

```python
1 + 12 + (-5) + (-6) = 2
```

So:

```python
window_sum = 2
max_sum = 2
```

---

### Step 2: Slide the window right

Now move the window one step right.

Old window:

```python
[1, 12, -5, -6]
```

New window:

```python
[12, -5, -6, 50]
```

Notice what changed:

- `1` left the window
- `50` entered the window

So instead of recomputing the whole sum, we do:

```python
new_sum = old_sum - outgoing + incoming
```

That is:

```python
new_sum = 2 - 1 + 50 = 51
```

So the new window sum is `51`.

Update:

```python
max_sum = max(2, 51) = 51
```

---

### Step 3: Slide again

Old window:

```python
[12, -5, -6, 50]
```

New window:

```python
[-5, -6, 50, 3]
```

What changed?

- `12` left
- `3` entered

So:

```python
new_sum = 51 - 12 + 3 = 42
```

Update:

```python
max_sum = max(51, 42) = 51
```

---

## Final Answer

```python
max_sum / k = 51 / 4 = 12.75
```

---

## Most Important Line

```python
window_sum += nums[right] - nums[right - k]
```

This is the heart of the sliding window.

Let’s break it down.

### `nums[right]`

This is the new element entering the window from the right.

### `nums[right - k]`

This is the old element leaving the window from the left.

So this line means:

```python
new_window_sum = old_window_sum + incoming - outgoing
```

---

## Why is `right - k` the outgoing element?

Suppose:

```python
nums = [1, 12, -5, -6, 50, 3]
k = 4
```

When `right = 4`, the new element is:

```python
nums[4] = 50
```

The old window covered indices:

```python
0, 1, 2, 3
```

The new window covers:

```python
1, 2, 3, 4
```

So the element that leaves is index `0`.

And:

```python
right - k = 4 - 4 = 0
```

So:

```python
nums[right - k]
```

correctly gives the outgoing element.

---

## Full Dry Run

### Input

```python
nums = [1, 12, -5, -6, 50, 3]
k = 4
```

### Initial window

```python
[1, 12, -5, -6]
sum = 2
max_sum = 2
```

---

### Move `right = 4`

Incoming:

```python
nums[4] = 50
```

Outgoing:

```python
nums[4 - 4] = nums[0] = 1
```

Update:

```python
window_sum = 2 + 50 - 1 = 51
max_sum = max(2, 51) = 51
```

Current window:

```python
[12, -5, -6, 50]
```

---

### Move `right = 5`

Incoming:

```python
nums[5] = 3
```

Outgoing:

```python
nums[5 - 4] = nums[1] = 12
```

Update:

```python
window_sum = 51 + 3 - 12 = 42
max_sum = max(51, 42) = 51
```

Current window:

```python
[-5, -6, 50, 3]
```

---

### Done

Return:

```python
51 / 4 = 12.75
```

---

## Why This Is Better Than Brute Force

### Brute force

For every window, recalculate the full sum.

Time:

```python
O(n * k)
```

### Sliding window

Each step updates the sum in constant time.

Time:

```python
O(n)
```

Space:

```python
O(1)
```

---

## Pattern to Remember

This problem is the classic **fixed-size sliding window** pattern.

Whenever the problem says:

- subarray of size exactly `k`
- substring of size exactly `k`
- find max/min/sum/count over every window of length `k`

you should think:

```python
window_sum += nums[right] - nums[right - k]
```

---

## Final Code

```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        window_sum = sum(nums[:k])
        max_sum = window_sum

        for right in range(k, len(nums)):
            window_sum += nums[right] - nums[right - k]
            max_sum = max(max_sum, window_sum)

        return max_sum / k
```

---

## Simple Intuition in One Sentence

When the window moves right by 1:

- one number enters
- one number leaves

So we update the sum instead of recomputing it.

That is why sliding window is efficient.

---

## Complexity

### Time

```python
O(n)
```

### Space

```python
O(1)
```

---

## Summary

- The subarray size is fixed at `k`
- Compute the first window sum
- Slide the window one step at a time
- Add the new element
- Remove the old element
- Track the maximum sum
- Return `max_sum / k`

This is one of the most basic and important sliding window problems.
