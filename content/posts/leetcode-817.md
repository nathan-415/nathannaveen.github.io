---
title: "Leetcode 817"
date: 2021-07-06T18:25:21-05:00
toc: false
images:
tags: [leetcode, golang, linked list]
---

[817. Linked List Components](https://leetcode.com/problems/linked-list-components/)

The idea of this solution is:

* We make a map to store all the values in `nums` because all the values in `nums` are unordered subsets of our linked list, so finding whether `nums` contains a value is now done in `O(1)` time (Note that to get all the values into the map it takes `O(n)` time).
* Then all we have to do is loop through our linked list and if `m` (Our map is called `m`) contains the current value and it doesn't contain the previous value or the value is the head and `m` contains the value we know that we have another component.

``` go
func numComponents(head *ListNode, nums []int) int {
    m := make(map[int] int)
    res := 0
    prev := head
    cur := head
    
    for _, num := range nums {
        m[num] = 1
    }
    
    for cur != nil {
        if m[cur.Val] == 1 && (cur == head || m[prev.Val] == 0) {
            res++
        }
        prev = cur
        cur = cur.Next
    }
    
    return res
}
```