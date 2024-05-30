###### **本文主要解析LeetCode在2024年5月26日10:30组织的第【399】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-399)**。**

---

### 题目一、[优质数对的总数 I](https://leetcode.cn/contest/weekly-contest-399/problems/find-the-number-of-good-pairs-i/)【简单】

#### 题目描述

给你两个整数数组 `nums1` 和 `nums2`，长度分别为 `n` 和 `m`。同时给你一个**正整数** `k`。

如果 `nums1[i]` 可以被 `nums2[j] * k` 整除，则称数对 `(i, j)` 为 **优质数对**（`0 <= i <= n - 1`, `0 <= j <= m - 1`）。

返回 **优质数对** 的总数。

 

**示例 1：**

**输入：**nums1 = [1,3,4], nums2 = [1,3,4], k = 1

**输出：**5

**解释：**

5个优质数对分别是 `(0, 0)`, `(1, 0)`, `(1, 1)`, `(2, 0)`, 和 `(2, 2)`。

**示例 2：**

**输入：**nums1 = [1,2,4,12], nums2 = [2,4], k = 3

**输出：**2

**解释：**

2个优质数对分别是 `(3, 0)` 和 `(3, 1)`。

 

**提示：**

- `1 <= n, m <= 50`
- `1 <= nums1[i], nums2[j] <= 50`
- `1 <= k <= 50`

#### 分析

简单题，按照题意模拟即可

#### 代码

```python
class Solution:
    def numberOfPairs(self, nums1: List[int], nums2: List[int], k: int) -> int:
        res = 0
        for num2 in nums2:
            for num1 in nums1:
                res += num1 % (k * num2) == 0
        return res
```



------

### 题目二、【中等】

#### 题目描述





#### 分析





#### 代码

```Python

```

------

### 题目三、【中等】

#### 题目描述



#### 分析



#### 代码

```python

```

------

### 题目四、【困难】

#### 题目描述



#### 分析



#### 代码

```python

```

