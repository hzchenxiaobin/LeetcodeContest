###### **本文主要解析LeetCode在2023年8月13日10:30组织的第【358】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-358)**。**

---

### 题目一、[数组中的最大数对和](https://leetcode.cn/contest/weekly-contest-358/problems/max-pair-sum-in-an-array/)【简单】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 。请你从 `nums` 中找出和 **最大** 的一对数，且这两个数数位上最大的数字相等。

返回最大和，如果不存在满足题意的数字对，返回 `-1` *。*

 

**示例 1：**

```
输入：nums = [51,71,17,24,42]
输出：88
解释：
i = 1 和 j = 2 ，nums[i] 和 nums[j] 数位上最大的数字相等，且这一对的总和 71 + 17 = 88 。 
i = 3 和 j = 4 ，nums[i] 和 nums[j] 数位上最大的数字相等，且这一对的总和 24 + 42 = 66 。
可以证明不存在其他数对满足数位上最大的数字相等，所以答案是 88 。
```

**示例 2：**

```
输入：nums = [1,2,3,4]
输出：-1
解释：不存在数对满足数位上最大的数字相等。
```

 

**提示：**

- `2 <= nums.length <= 100`
- `1 <= nums[i] <= 10^4`

#### 分析

数据量比较小，直接for循环模拟即可

#### 代码

```python
class Solution:
    def maxSum(self, nums: List[int]) -> int:
        n = len(nums)
        res = -1
        for i in range(n):
            for j in range(i+1, n):
                if max(list(str(nums[i]))) == max(list(str(nums[j]))):
                    res = max(nums[i] + nums[j], res)
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

