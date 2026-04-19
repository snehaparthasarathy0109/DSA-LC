Yes — this should be solved with a **fixed-size sliding window**.

Here’s the clean solution for **2461. Maximum Sum of Distinct Subarrays With Length K**:

```python
class Solution:
    def maximumSubarraySum(self, nums: List[int], k: int) -> int:
        freq = {}
        curr_sum = 0
        max_sum = 0
        left = 0

        for right in range(len(nums)):
            # add new element
            curr_sum += nums[right]
            freq[nums[right]] = freq.get(nums[right], 0) + 1

            # keep window size exactly k
            if right - left + 1 > k:
                freq[nums[left]] -= 1
                curr_sum -= nums[left]
                if freq[nums[left]] == 0:
                    del freq[nums[left]]
                left += 1

            # if window size is k and all elements are distinct
            if right - left + 1 == k and len(freq) == k:
                max_sum = max(max_sum, curr_sum)

        return max_sum
```

## Why this works

We need a subarray:

* of **exactly length `k`**
* with **all distinct elements**
* and we want the **maximum sum**

So for each window, we track:

* `curr_sum` → sum of current window
* `freq` → how many times each number appears
* `len(freq) == k` → means all `k` elements are distinct

Because:

* window size is `k`
* number of distinct values is also `k`

That can only happen if every element appears once.

---

## Sliding window idea

As `right` moves:

* add `nums[right]`

If the window gets too big:

* remove `nums[left]`
* move `left`

Whenever the window size becomes exactly `k`:

* check if all elements are distinct
* if yes, update `max_sum`

---

## Dry run

For:

```python
nums = [1,5,4,2,9,9,9]
k = 3
```

Windows:

* `[1,5,4]` → distinct, sum = 10
* `[5,4,2]` → distinct, sum = 11
* `[4,2,9]` → distinct, sum = 15
* `[2,9,9]` → not distinct
* `[9,9,9]` → not distinct

Answer = `15`

---

## Time complexity

* `O(n)`

Each element enters and leaves the window at most once.

## Space complexity

* `O(k)`

The frequency map stores at most `k` elements.

If you want, I can also show the version that is **closest to the code style you were trying to write**.
