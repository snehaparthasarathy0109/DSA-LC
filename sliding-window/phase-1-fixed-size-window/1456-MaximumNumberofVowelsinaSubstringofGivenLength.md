````md
# 1456. Maximum Number of Vowels in a Substring of Given Length

## Problem

Given a string `s` and an integer `k`, return the maximum number of vowel letters in any substring of `s` with length `k`.

Vowels are:
- `'a'`
- `'e'`
- `'i'`
- `'o'`
- `'u'`

---

## Why this is sliding window

The problem asks for:

- a **substring**
- of **exact length `k`**
- and wants the **maximum** over all such substrings

That is the classic pattern for a **fixed-size sliding window**.

Instead of counting vowels from scratch for every substring of length `k`, we:

1. Count vowels in the first window
2. Slide the window one step right
3. Add the new character entering the window
4. Remove the old character leaving the window
5. Track the maximum count seen

---

## Brute Force Approach

Try every substring of length `k`, count vowels, and keep the maximum.

### Brute force code

```python
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        vowels = set("aeiou")
        ans = 0

        for i in range(len(s) - k + 1):
            count = 0
            for j in range(i, i + k):
                if s[j] in vowels:
                    count += 1
            ans = max(ans, count)

        return ans
````

### Time Complexity

For each window, we count up to `k` characters.

So total time is:

```python
O(n * k)
```

---

## Optimized Sliding Window Approach

### Key idea

We do not need to recount the whole substring each time.

When the window moves right by 1:

* one character enters
* one character leaves

So we update the vowel count in `O(1)` time.

### Solution

```python
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        vowels = set("aeiou")
        count = 0

        for i in range(k):
            if s[i] in vowels:
                count += 1

        ans = count

        for right in range(k, len(s)):
            if s[right] in vowels:
                count += 1
            if s[right - k] in vowels:
                count -= 1
            ans = max(ans, count)

        return ans
```

---

## How this works

### Step 1: Count vowels in the first window

Suppose:

```python
s = "abciiidef"
k = 3
```

First window is:

```python
"abc"
```

Vowels in `"abc"`:

* `a` is a vowel

So:

```python
count = 1
ans = 1
```

### Step 2: Slide the window right

Move from `"abc"` to `"bci"`.

What changed?

* `'a'` left the window
* `'i'` entered the window

So:

* subtract 1 if `'a'` was a vowel
* add 1 if `'i'` is a vowel

That updates the count without recomputing the whole window.

---

## Dry Run

### Input

```python
s = "abciiidef"
k = 3
```

### First window: `"abc"`

Vowels:

* `a` → yes
* `b` → no
* `c` → no

```python
count = 1
ans = 1
```

### Move right to `"bci"`

Incoming:

```python
s[3] = 'i'
```

Outgoing:

```python
s[0] = 'a'
```

Update:

* incoming `'i'` is vowel → `count += 1`
* outgoing `'a'` is vowel → `count -= 1`

So count stays:

```python
count = 1
ans = 1
```

### Move right to `"cii"`

Incoming:

```python
s[4] = 'i'
```

Outgoing:

```python
s[1] = 'b'
```

Update:

* `'i'` enters → `+1`
* `'b'` leaves → `0`

```python
count = 2
ans = 2
```

### Move right to `"iii"`

Incoming:

```python
s[5] = 'i'
```

Outgoing:

```python
s[2] = 'c'
```

Update:

* `'i'` enters → `+1`
* `'c'` leaves → `0`

```python
count = 3
ans = 3
```

### Move right to `"iid"`

Incoming:

```python
s[6] = 'd'
```

Outgoing:

```python
s[3] = 'i'
```

Update:

* `'d'` enters → `0`
* `'i'` leaves → `-1`

```python
count = 2
ans = 3
```

### Move right to `"ide"`

Incoming:

```python
s[7] = 'e'
```

Outgoing:

```python
s[4] = 'i'
```

Update:

* `'e'` enters → `+1`
* `'i'` leaves → `-1`

```python
count = 2
ans = 3
```

### Move right to `"def"`

Incoming:

```python
s[8] = 'f'
```

Outgoing:

```python
s[5] = 'i'
```

Update:

* `'f'` enters → `0`
* `'i'` leaves → `-1`

```python
count = 1
ans = 3
```

### Final answer

```python
3
```

---

## Why `right - k`?

When the window ends at index `right`, its length is `k`.

So the character leaving the window is the one at:

```python
right - k
```

Because that was the leftmost character of the previous window.

---

## Important pattern

For fixed-size sliding window:

* add the incoming element
* remove the outgoing element

Here:

```python
if s[right] in vowels:
    count += 1
if s[right - k] in vowels:
    count -= 1
```

---

## Time Complexity

```python
O(n)
```

We scan the string once.

## Space Complexity

```python
O(1)
```

The vowel set has constant size.

---

## Final Code

```python
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        vowels = set("aeiou")
        count = 0

        for i in range(k):
            if s[i] in vowels:
                count += 1

        ans = count

        for right in range(k, len(s)):
            if s[right] in vowels:
                count += 1
            if s[right - k] in vowels:
                count -= 1
            ans = max(ans, count)

        return ans
```

---

## Simpler version using a helper count

```python
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        vowels = set("aeiou")
        count = sum(1 for i in range(k) if s[i] in vowels)
        ans = count

        for right in range(k, len(s)):
            if s[right] in vowels:
                count += 1
            if s[right - k] in vowels:
                count -= 1
            ans = max(ans, count)

        return ans
```

---

## One-line intuition

This is sliding window because we are checking every substring of fixed length `k`, and when the window moves, only one character enters and one character leaves.

```
```
