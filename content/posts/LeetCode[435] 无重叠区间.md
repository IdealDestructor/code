---
title: "LeetCode[435] 无重叠区间"
date: 2022-06-13 14:22:35
tags: [贪心算法]
categories: [LeetCode]
description: ""
slug: ""
authors: []
externalLink: ""
series: []
---

### Problem:

- 给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

  注意: 可以认为区间的终点总是大于它的起点。 区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。

  示例 1:

  - 输入: [ [1,2], [2,3], [3,4], [1,3] ]
  - 输出: 1
  - 解释: 移除 [1,3] 后，剩下的区间没有重叠。

  示例 2:

  - 输入: [ [1,2], [1,2], [1,2] ]
  - 输出: 2
  - 解释: 你需要移除两个 [1,2] 来使剩下的区间没有重叠。
  
  示例 3:
  
  - 输入: [ [1,2], [2,3] ]
  - 输出: 0
  - 解释: 你不需要移除任何区间，因为它们已经是无重叠的了。
  
  

<!--more-->

### Solution:

https://programmercarl.com/0435.无重叠区间.html

```javascript
var eraseOverlapIntervals = function(intervals) {
    intervals.sort((a, b) => { 
        return a[1] - b[1]
    })

    let count = 1
    let end = intervals[0][1]
    for (let i = 1; i < intervals.length; i++) {
        let interval = intervals[i]
        if (interval[0] >= end) {
            count++
            end = interval[1]
        }
    }
    return intervals.length - count
};
```