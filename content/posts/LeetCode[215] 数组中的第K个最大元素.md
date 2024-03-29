---
title: "LeetCode[215] 数组中的第K个最大元素"
date: 2021-03-26 11:29:45
tags: [堆排序]
categories: [LeetCode]
description: ""
slug: ""
authors: []
externalLink: ""
series: []
---

---
Related Topics:
  "数组": https://leetcode.com/tag/array/
  "分治": https://leetcode.com/tag/divide-and-conquer/
  "快速选择": https://leetcode.com/tag/quickselect/
  "排序": https://leetcode.com/tag/sorting/
  "堆（优先队列）": https://leetcode.com/tag/heap-priority-queue/
Similar Questions:
  "摆动排序 II": https://leetcode.com/problems/wiggle-sort-ii/
  "前 K 个高频元素": https://leetcode.com/problems/top-k-frequent-elements/
  "第三大的数": https://leetcode.com/problems/third-maximum-number/
  "数据流中的第 K 大元素": https://leetcode.com/problems/kth-largest-element-in-a-stream/
  "最接近原点的 K 个点": https://leetcode.com/problems/k-closest-points-to-origin/

### Problem:

给定整数数组 `nums` 和整数 `k`，请返回数组中第 `**k**` 个最大的元素。

请注意，你需要找的是数组排序后的第 `k` 个最大的元素，而不是第 `k` 个不同的元素。

**示例 1:**

```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2:**

```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

**提示：**

- `1 <= k <= nums.length <= 104`
- `-104 <= nums[i] <= 104`

<!--more-->

### Solution:

https://leetcode-cn.com/problems/kth-largest-element-in-an-array/solution/shu-zu-zhong-de-di-kge-zui-da-yuan-su-by-leetcode-/

方法一：基于快速排序的选择方法

我们可以改进快速排序算法来解决这个问题：在分解的过程当中，我们会对子数组进行划分，如果划分得到的q 正好就是我们需要的下标，就直接返回a[q]；否则，如果 q 比目标下标小，就递归右子区间，否则递归左子区间。这样就可以把原来递归两个区间变成只递归一个区间，提高了时间效率。这就是「快速选择」算法。

我们知道快速排序的性能和「划分」出的子数组的长度密切相关。直观地理解如果每次规模为 n 的问题我们都划分成 1 和 n−1，每次递归的时候又向 n−1 的集合中递归，这种情况是最坏的，时间代价是 O(n 2)。我们可以引入随机化来加速这个过程，它的时间代价的期望是 O(n)，证明过程可以参考「《算法导论》9.2：期望为线性的选择算法」。



方法二：基于堆排序的选择方法

思路和算法

我们也可以使用堆排序来解决这个问题——建立一个大根堆，做 k−1 次删除操作后堆顶元素就是我们要找的答案。在很多语言中，都有优先队列或者堆的的容器可以直接使用，但是在面试中，面试官更倾向于让更面试者自己实现一个堆。所以建议读者掌握这里大根堆的实现方法，在这道题中尤其要搞懂「建堆」、「调整」和「删除」的过程。



```c++
/*
 * @lc app=leetcode.cn id=215 lang=cpp
 *
 * [215] 数组中的第K个最大元素
 */

// @lc code=start
//基于快速排序的选择方法
// class Solution {
// public:
//     int quickSelect(vector<int>& a, int l, int r, int index) {
//         int q = randomPartition(a, l, r);
//         if (q == index) {
//             return a[q];
//         } else {
//             return q < index ? quickSelect(a, q + 1, r, index) : quickSelect(a, l, q - 1, index);
//         }
//     }

//     inline int randomPartition(vector<int>& a, int l, int r) {
//         int i = rand() % (r - l + 1) + l;
//         swap(a[i], a[r]);
//         return partition(a, l, r);
//     }

//     inline int partition(vector<int>& a, int l, int r) {
//         int x = a[r], i = l - 1;
//         for (int j = l; j < r; ++j) {
//             if (a[j] <= x) {
//                 swap(a[++i], a[j]);
//             }
//         }
//         swap(a[i + 1], a[r]);
//         return i + 1;
//     }

//     int findKthLargest(vector<int>& nums, int k) {
//         srand(time(0));
//         return quickSelect(nums, 0, nums.size() - 1, nums.size() - k);
//     }
// };
// 基于堆排序的选择方法
class Solution {
public:
    void maxHeapify(vector<int>& a, int i, int heapSize) {
        int l = i * 2 + 1, r = i * 2 + 2, largest = i;
        if (l < heapSize && a[l] > a[largest]) {
            largest = l;
        } 
        if (r < heapSize && a[r] > a[largest]) {
            largest = r;
        }
        if (largest != i) {
            swap(a[i], a[largest]);
            maxHeapify(a, largest, heapSize);
        }
    }

    void buildMaxHeap(vector<int>& a, int heapSize) {
        for (int i = heapSize / 2; i >= 0; --i) {
            maxHeapify(a, i, heapSize);
        } 
    }

    int findKthLargest(vector<int>& nums, int k) {
        int heapSize = nums.size();
        buildMaxHeap(nums, heapSize);
        for (int i = nums.size() - 1; i >= nums.size() - k + 1; --i) {
            swap(nums[0], nums[i]);
            --heapSize;
            maxHeapify(nums, 0, heapSize);
        }
        return nums[0];
    }
};
// @lc code=end


```

