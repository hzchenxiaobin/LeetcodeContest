###### **本文主要解析LeetCode在2024年5月26日10:30组织的第【398】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-398)**。**

---

### 题目一、[特殊数组 I](https://leetcode.cn/contest/weekly-contest-398/problems/special-array-i/)【简单】

#### 题目描述

如果数组的每一对相邻元素都是两个奇偶性不同的数字，则该数组被认为是一个 **特殊数组** 。

Aging 有一个整数数组 `nums`。如果 `nums` 是一个 **特殊数组** ，返回 `true`，否则返回 `false`。

 

**示例 1：**

**输入：**nums = [1]

**输出：**true

**解释：**

只有一个元素，所以答案为 `true`。

**示例 2：**

**输入：**nums = [2,1,4]

**输出：**true

**解释：**

只有两对相邻元素： `(2,1)` 和 `(1,4)`，它们都包含了奇偶性不同的数字，因此答案为 `true`。

**示例 3：**

**输入：**nums = [4,3,1,6]

**输出：**false

**解释：**

`nums[1]` 和 `nums[2]` 都是奇数。因此答案为 `false`。

 

**提示：**

- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`



#### 分析

数据量比较小，逐个判断即可。



#### 代码

```python
class Solution:
    def isArraySpecial(self, nums: List[int]) -> bool:
        return all(nums[i-1]&1 != nums[i]&1 for i in range(1,len(nums)))
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

