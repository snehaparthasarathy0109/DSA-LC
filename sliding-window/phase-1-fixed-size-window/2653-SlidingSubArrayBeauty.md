This is a **fixed-size sliding window + frequency counting** problem.

The trick is:

* each window has size `k`
* for each window, we need the **x-th smallest negative number**
* constraints for this problem make it easier because `nums[i]` is in the small range **[-50, 50]** on LeetCode, so we can track counts of negative values instead of sorting every window

---

## Key idea

For every window of size `k`:

* keep counts of negative numbers from `-50` to `-1`
* when the window is ready, scan from `-50` upward
* count how many negatives we have seen
* once we reach the `x`-th negative, that value is the beauty
* if we never reach `x`, answer is `0`

Because the value range is tiny, scanning `-50 ... -1` is basically constant time.

---

## Python solution

```python
class Solution:
    def getSubarrayBeauty(self, nums: List[int], k: int, x: int) -> List[int]:
        freq = [0] * 51   # freq[v] means count of -v
        result = []

        left = 0
        for right in range(len(nums)):
            if nums[right] < 0:
                freq[-nums[right]] += 1

            if right - left + 1 > k:
                if nums[left] < 0:
                    freq[-nums[left]] -= 1
                left += 1

            if right - left + 1 == k:
                count = 0
                beauty = 0

                for v in range(50, 0, -1):   # corresponds to -50, -49, ..., -1
                    count += freq[v]
                    if count >= x:
                        beauty = -v
                        break

                result.append(beauty)

        return result
```

---

## Why `range(50, 0, -1)`?

We want to check negatives in sorted order:

[
-50, -49, -48, \dots, -1
]

If `freq[v]` stores the count of `-v`, then:

* `v = 50` means number `-50`
* `v = 49` means number `-49`
* ...
* `v = 1` means number `-1`

So scanning:

```python
for v in range(50, 0, -1):
```

means we are checking negatives from smallest to largest.

---

## Dry run

### Example 1

```python
nums = [1,-1,-3,-2,3]
k = 3
x = 2
```

### Window 1: `[1, -1, -3]`

Negatives are:

```python
[-3, -1]
```

Sorted negatives: `[-3, -1]`

2nd smallest = `-1`

So answer starts with:

```python
[-1]
```

---

### Window 2: `[-1, -3, -2]`

Negatives are:

```python
[-1, -3, -2]
```

Sorted:

```python
[-3, -2, -1]
```

2nd smallest = `-2`

Answer:

```python
[-1, -2]
```

---

### Window 3: `[-3, -2, 3]`

Negatives are:

```python
[-3, -2]
```

Sorted:

```python
[-3, -2]
```

2nd smallest = `-2`

Final answer:

```python
[-1, -2, -2]
```

---

## Why this is sliding window

This is sliding window because:

* we are looking at every **subarray of size `k`**
* subarray means contiguous
* size `k` means fixed-size window
* when the window moves:

  * one element enters
  * one element leaves

So we update counts instead of rebuilding from scratch.

---

## Time complexity

For each position:

* add/remove from the window in `O(1)`
* scan the negative range `[-50, -1]`, which is only 50 values, so `O(50)` = constant

Total:

```python
O(n * 50) = O(n)
```

## Space complexity

```python
O(51) = O(1)
```

---

## Interview intuition

A brute-force approach would:

* take every window of size `k`
* sort it or extract negatives
* find the x-th smallest negative

That would be too slow.

The optimization is noticing:

* window size is fixed → sliding window
* value range is tiny → frequency array instead of sorting

---

## If you want the pattern in one sentence

This problem is:

> fixed-size sliding window + count the small negative value range to find the x-th smallest negative in each window.

I can also generate the full explanation in `.md` format like the previous ones.
