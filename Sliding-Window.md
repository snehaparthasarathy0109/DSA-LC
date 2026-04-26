# Sliding Window Problems

LeetCode currently has an official **Sliding Window** problem list page, and it shows **240** problems on the page right now. ([LeetCode](https://leetcode.com/problem-list/sliding-window/))

Trying to brute-force all 240 at once is not the fastest way to get good. The better route is to master the core variants first, then expand outward. Two widely shared LeetCode discussion lists group the most important starter and intermediate sliding-window problems, including classics like **Longest Substring Without Repeating Characters**, **Minimum Size Subarray Sum**, **Sliding Window Maximum**, **Fruit Into Baskets**, **Subarrays with K Different Integers**, and **Longest Repeating Character Replacement**. ([LeetCode](https://leetcode.com/discuss/post/3630462/top-20-sliding-window-problems-for-begin-zgm5/?utm_source=chatgpt.com))

Here's the set I'd use to get **extremely familiar** with the pattern.

## Phase 1: fixed-size window

These teach "add right, remove left" without complex shrinking logic.

* 643. Maximum Average Subarray I
* 1423. Maximum Points You Can Obtain from Cards
* 1456. Maximum Number of Vowels in a Substring of Given Length
* 2461. Maximum Sum of Distinct Subarrays With Length K
* 2653. Sliding Subarray Beauty

## Phase 2: basic variable-size window

These teach the classic expand-then-shrink pattern.

* 209. Minimum Size Subarray Sum
* 3. Longest Substring Without Repeating Characters
* 713. Subarray Product Less Than K
* 1208. Get Equal Substrings Within Budget
* 904. Fruit Into Baskets

## Phase 3: "at most K" / "exactly K"

This is the most important family to recognize.

* 340. Longest Substring with At Most K Distinct Characters
* 159. Longest Substring with At Most Two Distinct Characters
* 992. Subarrays with K Different Integers
* 1248. Count Number of Nice Subarrays
* 930. Binary Subarrays With Sum

## Phase 4: frequency-map / replacement windows

These force you to track counts carefully.

* 424. Longest Repeating Character Replacement
* 76. Minimum Window Substring
* 567. Permutation in String
* 438. Find All Anagrams in a String
* 1234. Replace the Substring for Balanced String

## Phase 5: monotonic deque windows

These are still "window" problems, but the real trick is the data structure.

* 239. Sliding Window Maximum
* 1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit
* 862. Shortest Subarray with Sum at Least K
* 480. Sliding Window Median

## Phase 6: transformed-window / trick questions

These make you recognize that the window may be on the complement, not the direct target.

* 1658. Minimum Operations to Reduce X to Zero
* 1004. Max Consecutive Ones III
* 2024. Maximize the Confusion of an Exam
* 1838. Frequency of the Most Frequent Element
* 2762. Continuous Subarrays
* 2962. Count Subarrays Where Max Element Appears at Least K Times
* 2537. Count the Number of Good Subarrays
* 2799. Count Complete Subarrays in an Array
* 2401. Longest Nice Subarray
* 2134. Minimum Swaps to Group All 1's Together II

## What to recognize in any sliding-window problem

Almost every sliding-window problem reduces to one of these prompts:

* **Fixed-size:** "find best/count over every subarray of length k"
* **Longest valid window:** "maximize length while condition stays true"
* **Shortest valid window:** "minimize length once condition becomes true"
* **At most K:** count/length with a bounded property
* **Exactly K:** usually compute `atMost(K) - atMost(K-1)`
* **Window + deque:** need max/min in O(1) while moving
* **Window + prefix/deque hybrid:** when negatives break normal shrinking logic

## Best study order

Do them in this order:

1. 643
2. 209
3. 3
4. 713
5. 904
6. 424
7. 567
8. 438
9. 76
10. 1004
11. 340
12. 992
13. 1248
14. 239
15. 1438
16. 1658
17. 1838
18. 862
19. 480
20. 2762

If you can solve those cleanly, you'll recognize most sliding-window interviews immediately.

## The real goal

You do **not** need all 240. You need to deeply internalize about **20–30 representative problems**. That's also how the strongest community LeetCode sliding-window lists are structured: a smaller grouped set of high-value problems rather than brute-forcing the entire tag. ([LeetCode](https://leetcode.com/discuss/post/3630462/top-20-sliding-window-problems-for-begin-zgm5/?utm_source=chatgpt.com))

Use the official LeetCode sliding-window page as your full backlog, since it is the current authoritative source for the full tag/list. ([LeetCode](https://leetcode.com/problem-list/sliding-window/))

I can turn this into a **30-day sliding-window curriculum** with problem order, pattern notes, and what each problem teaches.
