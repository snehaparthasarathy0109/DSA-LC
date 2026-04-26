I can’t reliably extract every current problem title from LeetCode’s dynamic “Two Pointers” page in this environment, so I don’t want to pretend this is the full official catalog. The authoritative source for the live list is LeetCode’s **Two Pointers** page. ([LeetCode][1])

What I *can* do is give you a strong, interview-focused two-pointers curriculum that covers the major subpatterns people repeatedly use: opposite ends, same-direction windows, slow/fast pointers, in-place write pointers, sort+two-pointers, and center expansion. Those categories line up with common LeetCode study/discussion breakdowns. ([LeetCode][2])

## How to recognize two pointers in interviews

Think “two pointers” when you see one of these:

* sorted array + find pair/triplet/closest/smaller
* substring/subarray with a moving left boundary
* in-place compaction or overwrite
* linked list cycle / middle / nth-from-end
* palindrome / compare from both ends
* expand-around-center for palindromes
* count subarrays by maintaining a valid range

## Practice order that builds the pattern

### 1) Start with opposite-ends pointers

These teach the raw pointer movement idea.

* 125. Valid Palindrome
* 167. Two Sum II - Input Array Is Sorted
* 344. Reverse String
* 680. Valid Palindrome II
* 11. Container With Most Water
* 881. Boats to Save People
* 977. Squares of a Sorted Array
* 88. Merge Sorted Array
* 392. Is Subsequence
* 844. Backspace String Compare

### 2) In-place overwrite / write-pointer problems

These teach “read pointer + write pointer”.

* 26. Remove Duplicates from Sorted Array
* 27. Remove Element
* 80. Remove Duplicates from Sorted Array II
* 283. Move Zeroes
* 75. Sort Colors
* 905. Sort Array By Parity
* 1089. Duplicate Zeros

### 3) Sort + two pointers for pairs/triplets

These are extremely interview-relevant.

* 15. 3Sum
* 16. 3Sum Closest
* 18. 4Sum
* 259. 3Sum Smaller
* 611. Valid Triangle Number
* 923. 3Sum With Multiplicity
* 1498. Number of Subsequences That Satisfy the Given Sum Condition

### 4) Same-direction pointers / sliding-window style

These overlap with sliding window, and many interviewers mentally group them under two pointers.

* 3. Longest Substring Without Repeating Characters
* 209. Minimum Size Subarray Sum
* 713. Subarray Product Less Than K
* 904. Fruit Into Baskets
* 340. Longest Substring with At Most K Distinct Characters
* 159. Longest Substring with At Most Two Distinct Characters
* 424. Longest Repeating Character Replacement
* 567. Permutation in String
* 438. Find All Anagrams in a String
* 76. Minimum Window Substring
* 1004. Max Consecutive Ones III
* 1208. Get Equal Substrings Within Budget
* 1248. Count Number of Nice Subarrays
* 930. Binary Subarrays With Sum
* 992. Subarrays with K Different Integers
* 1493. Longest Subarray of 1’s After Deleting One Element
* 2024. Maximize the Confusion of an Exam
* 2762. Continuous Subarrays

### 5) Fast and slow pointers

These teach “different speeds” rather than a window.

* 141. Linked List Cycle
* 142. Linked List Cycle II
* 876. Middle of the Linked List
* 19. Remove Nth Node From End of List
* 234. Palindrome Linked List
* 287. Find the Duplicate Number
* 457. Circular Array Loop
* 61. Rotate List
* 143. Reorder List

### 6) Expand around center

These are still a two-pointer pattern, just starting from the middle.

* 5. Longest Palindromic Substring
* 647. Palindromic Substrings

### 7) Good stretch problems after the basics

These make pattern recognition sharper.

* 986. Interval List Intersections
* 658. Find K Closest Elements
* 826. Most Profit Assigning Work
* 1537. Get the Maximum Score
* 1574. Shortest Subarray to be Removed to Make Array Sorted
* 1616. Split Two Strings to Make Palindrome
* 1658. Minimum Operations to Reduce X to Zero
* 1768. Merge Strings Alternately
* 1793. Maximum Score of a Good Subarray
* 1868. Product of Two Run-Length Encoded Arrays

## The minimum set to truly “get” two pointers

If you only do 20 really well, do these:

* 125
* 167
* 344
* 680
* 11
* 26
* 27
* 283
* 75
* 15
* 16
* 18
* 3
* 209
* 713
* 904
* 424
* 141
* 19
* 5

If you can solve those cleanly, you will recognize most interview two-pointer prompts very quickly.

## What each subpattern feels like

Opposite ends:

* “I have a sorted array or symmetric string; moving one side changes the answer predictably.”

Same direction:

* “I keep a valid window; if it breaks, I move left until it’s fixed.”

Read/write:

* “I’m compacting, deleting, or rewriting in place.”

Fast/slow:

* “I need cycle detection, a midpoint, or relative distance.”

Sort + two pointers:

* “Fix one element, then solve the rest with left/right.”

Center expansion:

* “Try every center and expand while valid.”

## Best drilling strategy

Do them in waves:

* Wave 1: 125, 167, 344, 26, 27, 283
* Wave 2: 11, 75, 15, 16, 18
* Wave 3: 3, 209, 713, 904, 424
* Wave 4: 141, 19, 876, 234, 287
* Wave 5: 5, 647, 986, 658, 1574

After each problem, write down:

* how the pointers moved
* what invariant stayed true
* what condition forced a pointer to move
* why a brute force version would be slower

## One rule that helps a lot

Before coding, ask:

* What does the left pointer represent?
* What does the right pointer represent?
* When do I move left?
* When do I move right?
* What invariant am I preserving?

That is the difference between “memorizing solutions” and actually seeing the pattern.

The official live LeetCode two-pointers page is still the best place to pull the evolving complete catalog, while LeetCode discussions also break the pattern into opposite-ends, fast/slow, and sliding-window-like variants. ([LeetCode][1])

I can turn this into a **30-day two-pointers study plan** with daily problem order and pattern notes.

[1]: https://leetcode.com/problem-list/two-pointers/?utm_source=chatgpt.com "Two Pointers"
[2]: https://leetcode.com/discuss/post/1688903/solved-all-two-pointers-problems-in-100-z56cn/?utm_source=chatgpt.com "Solved all two pointers problems in 100 days. - Discuss"
