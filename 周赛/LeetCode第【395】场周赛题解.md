###### **本文主要解析LeetCode在2024年4月28日10:30组织的第【395】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-395)**。**

---

### 题目一、[找出与数组相加的整数 I](https://leetcode.cn/contest/weekly-contest-395/problems/find-the-integer-added-to-array-i/)【简单】

#### 题目描述

给你两个长度相等的数组 `nums1` 和 `nums2`。

数组 `nums1` 中的每个元素都与变量 `x` 所表示的整数相加。如果 `x` 为负数，则表现为元素值的减少。

在与 `x` 相加后，`nums1` 和 `nums2` **相等** 。当两个数组中包含相同的整数，并且这些整数出现的频次相同时，两个数组 **相等** 。

返回整数 `x` 。

 

**示例 1:**

**输入：**nums1 = [2,6,4], nums2 = [9,7,5]

**输出：**3

**解释：**

与 3 相加后，`nums1` 和 `nums2` 相等。

**示例 2:**

**输入：**nums1 = [10], nums2 = [5]

**输出：**-5

**解释：**

与 `-5` 相加后，`nums1` 和 `nums2` 相等。

**示例 3:**

**输入：**nums1 = [1,1,1,1], nums2 = [1,1,1,1]

**输出：**0

**解释：**

与 0 相加后，`nums1` 和 `nums2` 相等。

 

**提示：**

- `1 <= nums1.length == nums2.length <= 100`
- `0 <= nums1[i], nums2[i] <= 1000`
- 测试用例以这样的方式生成：存在一个整数 `x`，使得 `nums1` 中的每个元素都与 `x` 相加后，`nums1` 与 `nums2` 相等。

#### 分析

简单题，模拟即可

#### 代码

```python
class Solution:
    def addedInteger(self, nums1: List[int], nums2: List[int]) -> int:
        return min(nums2) - min(nums1)
```



------

### 题目二、[找出与数组相加的整数 II](https://leetcode.cn/contest/weekly-contest-395/problems/find-the-integer-added-to-array-ii/)【中等】

#### 题目描述

给你两个整数数组 `nums1` 和 `nums2`。

从 `nums1` 中移除两个元素，并且所有其他元素都与变量 `x` 所表示的整数相加。如果 `x` 为负数，则表现为元素值的减少。

执行上述操作后，`nums1` 和 `nums2` **相等** 。当两个数组中包含相同的整数，并且这些整数出现的频次相同时，两个数组 **相等** 。

返回能够实现数组相等的 **最小** 整数 `x` 。

 

**示例 1:**

**输入：**nums1 = [4,20,16,12,8], nums2 = [14,18,10]

**输出：**-2

**解释：**

移除 `nums1` 中下标为 `[0,4]` 的两个元素，并且每个元素与 `-2` 相加后，`nums1` 变为 `[18,14,10]` ，与 `nums2` 相等。

**示例 2:**

**输入：**nums1 = [3,5,5,3], nums2 = [7,7]

**输出：**2

**解释：**

移除 `nums1` 中下标为 `[0,3]` 的两个元素，并且每个元素与 `2` 相加后，`nums1` 变为 `[7,7]` ，与 `nums2` 相等。

 

**提示：**

- `3 <= nums1.length <= 200`
- `nums2.length == nums1.length - 2`
- `0 <= nums1[i], nums2[i] <= 1000`
- 测试用例以这样的方式生成：存在一个整数 `x`，`nums1` 中的每个元素都与 `x` 相加后，再移除两个元素，`nums1` 可以与 `nums2` 相等。



#### 分析

数据量比较小，可以枚举所有的两个元素的可能，删除那两个元素，再求最小的整数。



#### 代码

```Python
class Solution:
    def minimumAddedInteger(self, nums1: List[int], nums2: List[int]) -> int:
        nums1.sort()
        nums2.sort()
        n = len(nums1)
        res = inf
        for i in range(0, n):
            for j in range(i+1, n):
                nums = [nums1[k] for k in range(0, n) if k != i and k != j]
                p = nums2[0] - nums[0]
                flag = True
                for k in range(0, n-2):
                    if nums2[k] - nums[k] != p:
                        flag = False
                        break
                if flag:
                    res = min(p, res)
        return res
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

