---
date: 2022-02-13 14:22:35
tags: [动态规划]
title: "LeetCode[72] 编辑距离"
description: ""
slug: ""
authors: []
categories: [编程算法]
externalLink: ""
series: []
---

Related Topics:

"字符串": https://leetcode.com/tag/string/

"动态规划": https://leetcode.com/tag/dynamic-programming/

Similar Questions:

"相隔为 1 的编辑距离": https://leetcode.com/problems/one-edit-distance/

 "两个字符串的删除操作": https://leetcode.com/problems/delete-operation-for-two-strings/

 "两个字符串的最小ASCII删除和": https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/

"不相交的线": https://leetcode.com/problems/uncrossed-lines/

### Problem:

给你两个单词 `word1` 和 `word2`，请你计算出将 `word1` 转换成 `word2`所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

- 插入一个字符
- 删除一个字符
- 替换一个字符

**示例 1：**

```
输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

**示例 2：**

```
输入：word1 = "intention", word2 = "execution"
输出：5
解释：
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```

**提示：**

- `0 <= word1.length, word2.length <= 500`
- `word1` 和 `word2` 由小写英文字母组成

<!--more-->

### Solution:

```c++
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();

        // 有一个字符串为空串
        if (n * m == 0) return n + m;

        // DP 数组
        int D[n + 1][m + 1];

        // 边界状态初始化
        for (int i = 0; i < n + 1; i++) {
            D[i][0] = i;
        }
        for (int j = 0; j < m + 1; j++) {
            D[0][j] = j;
        }

        // 计算所有 DP 值
        for (int i = 1; i < n + 1; i++) {
            for (int j = 1; j < m + 1; j++) {
                int left = D[i - 1][j] + 1;
                int down = D[i][j - 1] + 1;
                int left_down = D[i - 1][j - 1];
                if (word1[i - 1] != word2[j - 1]) left_down += 1;
                D[i][j] = min(left, min(down, left_down));
            }
        }
        return D[n][m];
    }
};
```
