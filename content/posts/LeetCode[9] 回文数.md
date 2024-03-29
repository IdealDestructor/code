---
title: "LeetCode[9] 回文数"
date: 2021-03-19 14:29:45
tags: [数学]
categories: [LeetCode]
description: ""
slug: ""
authors: []
externalLink: ""
series: []
---

### Related Topics:

"数学": https://leetcode.com/tag/math/ Similar Questions: "回文链表": https://leetcode.com/problems/palindrome-linked-list/

### Problem:

给你一个整数 `x` ，如果 `x` 是一个回文整数，返回 `true` ；否则，返回 `false` 。

回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。例如，`121` 是回文，而 `123` 不是。

**示例 1：**

```
输入：x = 121
输出：true
```

**示例 2：**

```
输入：x = -121
输出：false
解释：从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3：**

```
输入：x = 10
输出：false
解释：从右向左读, 为 01 。因此它不是一个回文数。
```

**示例 4：**

```
输入：x = -101
输出：false
```

**提示：**

- `231 <= x <= 231 - 1`
- *进阶：**你能不将整数转为字符串来解决这个问题吗？

<!--more-->

### Solution:

https://leetcode-cn.com/problems/palindrome-number/solution/hui-wen-shu-by-leetcode-solution/

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if(x < 0 || ( x != 0 && x % 10==0 ))
            return false;
        int revertedNumber = 0;
        while(x > revertedNumber){
            revertedNumber = revertedNumber * 10 + x % 10;
            x /= 10;
        }
        return x == revertedNumber || x == revertedNumber/10;
    }
};
```