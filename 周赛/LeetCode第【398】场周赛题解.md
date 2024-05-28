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

### 题目二、[特殊数组 II](https://leetcode.cn/contest/weekly-contest-398/problems/special-array-ii/)【中等】

#### 题目描述

如果数组的每一对相邻元素都是两个奇偶性不同的数字，则该数组被认为是一个 **特殊数组** 。

周洋哥有一个整数数组 `nums` 和一个二维整数矩阵 `queries`，对于 `queries[i] = [fromi, toi]`，请你帮助周洋哥检查子数组 `nums[fromi..toi]` 是不是一个 **特殊数组** 。

返回布尔数组 `answer`，如果 `nums[fromi..toi]` 是特殊数组，则 `answer[i]` 为 `true` ，否则，`answer[i]` 为 `false` 。

 

**示例 1：**

**输入：**nums = [3,4,1,2,6], queries = [[0,4]]

**输出：**[false]

**解释：**

子数组是 `[3,4,1,2,6]`。2 和 6 都是偶数。

**示例 2：**

**输入：**nums = [4,3,1,6], queries = [[0,2],[2,3]]

**输出：**[false,true]

**解释：**

1. 子数组是 `[4,3,1]`。3 和 1 都是奇数。因此这个查询的答案是 `false`。
2. 子数组是 `[1,6]`。只有一对：`(1,6)`，且包含了奇偶性不同的数字。因此这个查询的答案是 `true`。

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^5`
- `1 <= queries.length <= 10^5`
- `queries[i].length == 2`
- `0 <= queries[i][0] <= queries[i][1] <= nums.length - 1`

#### 分析

前缀和的思路

1.根据相邻的数字计算出当前位置是否是奇偶性不同的数字，如果是的话取1，如果不是则取0

示例2：[4, 3, 1, 6]  -> [1, 0, 0, 1]

2.求前缀和

示例2：[4, 3, 1, 6]  -> [1, 0, 0, 1] -> [1, 1, 1, 2]

3.根据查询的左端点l和右端点r，如果presum[r] - presum[l] + 1 = r - l + 1，则该区间内是连续的奇偶性

#### 代码

```Python
class Solution:
    def isArraySpecial(self, nums: List[int], queries: List[List[int]]) -> List[bool]:
        res = [ 1 if x%2 != y%2 else 0 for x, y in pairwise(nums)]
        pres = list(accumulate(res, initial=0))
        return [pres[r]-pres[l] == r-l for l, r in queries]
```

------

### 题目三、[所有数对中数位不同之和](https://leetcode.cn/contest/weekly-contest-398/problems/sum-of-digit-differences-of-all-pairs/)【中等】

#### 题目描述

车尔尼有一个数组 `nums` ，它只包含 **正** 整数，所有正整数的数位长度都 **相同** 。

两个整数的 **数位不同** 指的是两个整数 **相同** 位置上不同数字的数目。

请车尔尼返回 `nums` 中 **所有** 整数对里，**数位不同之和。**

 

**示例 1：**

**输入：**nums = [13,23,12]

**输出：**4

**解释：**
计算过程如下：
\- **1**3 和 **2**3 的数位不同为 1 。
\- 1**3** 和 1**2** 的数位不同为 1 。
\- **23** 和 **12** 的数位不同为 2 。
所以所有整数数对的数位不同之和为 `1 + 1 + 2 = 4` 。

**示例 2：**

**输入：**nums = [10,10,10,10]

**输出：**0

**解释：**
数组中所有整数都相同，所以所有整数数对的数位不同之和为 0 。

 

**提示：**

- `2 <= nums.length <= 10^5`
- `1 <= nums[i] < 10^9`
- `nums` 中的整数都有相同的数位长度。

#### 分析

1.计算出所有数对中数位之和

所有数对 * 每个数字的长度 -> math.comb(len(nums), 2) * 数字的长度

2.统计出所有数字每个位置上的元素

3减掉每个位置上相同的元素的组合个数

#### 代码

```python
class Solution:
    def sumDigitDifferences(self, nums: List[int]) -> int:
        num_list = [list(map(int, str(x))) for x in nums]
        m = len(num_list[0])
        ans = math.comb(len(nums), 2) * m
        for digits in zip(*num_list):
            counter = list(Counter(digits).values())
            ans -= sum(math.comb(x, 2) for x in counter)
        return ans
```

------

### 题目四、【困难】

#### 题目描述



#### 分析



#### 代码

```python

```

