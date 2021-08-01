---
date: "2021-08-01"
title: Solving the median of two sorted arrays in O (n log (m + n))
type: post
---

I have been doing a bit of HackerRank and LeetCode challenges to practice and avoid skill rot since I do not do as much low level programming as I used to. While going over the discussions for one of these challenges [1] I noticed a lot of people bragging about their simple solutions while also missing the entire point of the excercise.

The problem is described like this:

> Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.
> 
> The overall run time complexity should be O(log (m+n)).

Most of the solutions proposed do a variation of a merge and sort before finding the median. Something like this:

```python
nums = nums1 + nums2
nums.sort()
```

This is simple and easy to understand but it completely ignores the run time complexity. A sort is not faster than `O(n log (n))` [2] so there is no way for this solution to fulfill the time complexity requirement.

What the solution should do is to take advantage of the fact that both lists are already sorted. Assuming that the list length can be retrieved and the first element removed in `O(1)` time it is actually trivial to implement a faster merge.

```python
nums = []

while len(nums1) > 0 or len(nums2) > 0:
    if len(nums2) == 0 or (len(nums1) > 0 and nums1[0] < nums2[0]):
        nums.append(nums1.pop(0))
    else:
        nums.append(nums2.pop(0))
```

Calls to len() are `O(1)` [2]. But the calls to pop(0) are `O(n)` while pop() or pop(-1) are `O(1)` [3]. In other words it would be faster to merge the two lists backwards and then reverse the result rather than combining the lists in the right order from the start. Here is the same solution but forwards.

```python
nums = []

while len(nums1) > 0 or len(nums2) > 0:
    if len(nums2) == 0 or (len(nums1) > 0 and nums1[-1] > nums2[-1]):
        nums.append(nums1.pop())
    else:
        nums.append(nums2.pop())

nums.reverse()
```

This will require a single pass at `O(m + n)` time.

 1. https://leetcode.com/problems/median-of-two-sorted-arrays/
 2. https://wiki.python.org/moin/TimeComplexity
 3. https://thecodingbot.com/time-complexity-of-built-in-len-function-in-python/