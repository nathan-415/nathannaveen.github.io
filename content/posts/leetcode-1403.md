---
title: "Leetcode 1403"
date: 2021-06-16T11:22:07-05:00
toc: false
images:
tags: [leetcode, golang, math, array]
---

[1403. Minimum Subsequence in Non-Increasing Order](https://leetcode.com/problems/minimum-subsequence-in-non-increasing-order/)

The idea of this solution is pretty simple, we first sort `nums` in non-increasing order and then find the sum of `nums`. After that, we can loop through `nums` and subtract the greatest numbers in `nums` from the total sum and add the greatest numbers in `nums` to a different sum. And then, we append the `num` to `res` (the resulting function). If the other sum is greater than the total sum, we can break out of the loop and return `res`.

``` go
func minSubsequence(nums []int) []int {
	res := []int{}
	sum := 0
	resSum := 0
	sort.Slice(nums, func(i, j int) bool { return nums[i] > nums[j] })
	for _, num := range nums { sum += num }
	
	for _, num := range nums {
		sum -= num
		resSum += num
		res = append(res, num)
		if resSum > sum { break }
	}
	return res
}
```