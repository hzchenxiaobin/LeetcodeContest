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

### 题目二、[翻倍以链表形式表示的数字](https://leetcode.cn/contest/weekly-contest-358/problems/double-a-number-represented-as-a-linked-list/)【中等】

#### 题目描述

给你一个 **非空** 链表的头节点 `head` ，表示一个不含前导零的非负数整数。

将链表 **翻倍** 后，返回头节点 `head` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2023/05/28/example.png)

```
输入：head = [1,8,9]
输出：[3,7,8]
解释：上图中给出的链表，表示数字 189 。返回的链表表示数字 189 * 2 = 378 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2023/05/28/example2.png)

```
输入：head = [9,9,9]
输出：[1,9,9,8]
解释：上图中给出的链表，表示数字 999 。返回的链表表示数字 999 * 2 = 1998 。
```

 

**提示：**

- 链表中节点的数目在范围 `[1, 104]` 内
- `0 <= Node.val <= 9`
- 生成的输入满足：链表表示一个不含前导零的数字，除了数字 `0` 本身。

#### 分析

1.遍历链表获得数字

2.将数字除以2

3.将数字转成数组，构建链表

#### 代码

```Python
class Solution:
    def doubleIt(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # 1.遍历链表，计算数字
        num = 0
        node = head
        while node:
            num = num * 10 + node.val
            node = node.next
        
        # 2.将数字乘以2
        num *= 2
        if num == 0:
            return ListNode(0)
        
        # 3.构建返回链表
        res = None
        while num:
            res = ListNode(num % 10, res)
            num //= 10
        return res
```

------

### 题目三、[限制条件下元素之间的最小绝对差](https://leetcode.cn/contest/weekly-contest-358/problems/minimum-absolute-difference-between-elements-with-constraint/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 和一个整数 `x` 。

请你找到数组中下标距离至少为 `x` 的两个元素的 **差值绝对值** 的 **最小值** 。

换言之，请你找到两个下标 `i` 和 `j` ，满足 `abs(i - j) >= x` 且 `abs(nums[i] - nums[j])` 的值最小。

请你返回一个整数，表示下标距离至少为 `x` 的两个元素之间的差值绝对值的 **最小值** 。

 

**示例 1：**

```
输入：nums = [4,3,2,4], x = 2
输出：0
解释：我们选择 nums[0] = 4 和 nums[3] = 4 。
它们下标距离满足至少为 2 ，差值绝对值为最小值 0 。
0 是最优解。
```

**示例 2：**

```
输入：nums = [5,3,2,10,15], x = 1
输出：1
解释：我们选择 nums[1] = 3 和 nums[2] = 2 。
它们下标距离满足至少为 1 ，差值绝对值为最小值 1 。
1 是最优解。
```

**示例 3：**

```
输入：nums = [1,2,3,4], x = 3
输出：3
解释：我们选择 nums[0] = 1 和 nums[3] = 4 。
它们下标距离满足至少为 3 ，差值绝对值为最小值 3 。
3 是最优解。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^9`
- `0 <= x < nums.length`

#### 分析

二分法

1.从索引为x开始遍历，将小于等于i - x的队列索引的值加入有序队列

2.使用二分法找到离nums[i]最近的的索引

3.找到相减的最小值

#### 代码

```python
from sortedcontainers import SortedList

class Solution:
    def minAbsoluteDifference(self, nums: List[int], x: int) -> int:
        n = len(nums)
        sl = SortedList()
        res = max(nums)
        
        for i in range(x, n):
            sl.add(nums[i-x])
            pos = sl.bisect_left(nums[i])
            for j in [pos-1, pos, pos+1]:
                if 0 <= j < len(sl):
                    res = min(abs(sl[j] - nums[i]), res)
            
        return res
```

------

### 题目四、[操作使得分最大](https://leetcode.cn/contest/weekly-contest-358/problems/apply-operations-to-maximize-score/)【困难】

#### 题目描述

给你一个长度为 `n` 的正整数数组 `nums` 和一个整数 `k` 。

一开始，你的分数为 `1` 。你可以进行以下操作至多 `k` 次，目标是使你的分数最大：

- 选择一个之前没有选过的 **非空** 子数组 `nums[l, ..., r]` 。
- 从 `nums[l, ..., r]` 里面选择一个 **质数分数** 最高的元素 `x` 。如果多个元素质数分数相同且最高，选择下标最小的一个。
- 将你的分数乘以 `x` 。

`nums[l, ..., r]` 表示 `nums` 中起始下标为 `l` ，结束下标为 `r` 的子数组，两个端点都包含。

一个整数的 **质数分数** 等于 `x` 不同质因子的数目。比方说， `300` 的质数分数为 `3` ，因为 `300 = 2 * 2 * 3 * 5 * 5` 。

请你返回进行至多 `k` 次操作后，可以得到的 **最大分数** 。

由于答案可能很大，请你将结果对 `109 + 7` 取余后返回。

 

**示例 1：**

```
输入：nums = [8,3,9,3,8], k = 2
输出：81
解释：进行以下操作可以得到分数 81 ：
- 选择子数组 nums[2, ..., 2] 。nums[2] 是子数组中唯一的元素。所以我们将分数乘以 nums[2] ，分数变为 1 * 9 = 9 。
- 选择子数组 nums[2, ..., 3] 。nums[2] 和 nums[3] 质数分数都为 1 ，但是 nums[2] 下标更小。所以我们将分数乘以 nums[2] ，分数变为 9 * 9 = 81 。
81 是可以得到的最高得分。
```

**示例 2：**

```
输入：nums = [19,12,14,6,10,18], k = 3
输出：4788
解释：进行以下操作可以得到分数 4788 ：
- 选择子数组 nums[0, ..., 0] 。nums[0] 是子数组中唯一的元素。所以我们将分数乘以 nums[0] ，分数变为 1 * 19 = 19 。
- 选择子数组 nums[5, ..., 5] 。nums[5] 是子数组中唯一的元素。所以我们将分数乘以 nums[5] ，分数变为 19 * 18 = 342 。
- 选择子数组 nums[2, ..., 3] 。nums[2] 和 nums[3] 质数分数都为 2，但是 nums[2] 下标更小。所以我们将分数乘以 nums[2] ，分数变为  342 * 14 = 4788 。
4788 是可以得到的最高的分。
```

 

**提示：**

- `1 <= nums.length == n <= 10^5`
- `1 <= nums[i] <= 10^5`
- `1 <= k <= min(n * (n + 1) / 2, 10^9)`

#### 分析

1.预处理所有的数字的质分数个数

```python
x = 10 ** 5
score = [0 for i in range(x+1)]
for i in range(2, x+1):
    if score[i]:
        continue
    for j in range(i, x + 1, i):
        score[j] += 1
```

2.遍历元素，通过单调栈求出元素左边第一个**大于等于**当前元素质数分数的索引和右边第一个**大于**当前元素的质数分数的索引。

单调栈模板代码：

```python
stack = []
for num in nums:
    while stack and stack[-1] < num:
        stack.pop()
    stack.append(num)
```

3.从大到小排序元素并且遍历，通过相乘算出遍历到的元素出现的次数（对结果的影响次数）

count = (i - left) * (right - i)

4.通过快速幂计算结果

res *= pow(num, count, MOD) 

#### 代码

```python
MAX = 10 ** 5
prime_score = [0 for i in range(MAX + 1)]
for i in range(2, MAX + 1):
    if prime_score[i]:
        continue
    for j in range(i, MAX + 1, i):
        prime_score[j] += 1

class Solution:
    def maximumScore(self, nums: List[int], k: int) -> int:
        MOD = 10 ** 9 + 7
        n = len(nums)
        left = [-1 for i in range(n)]
        right = [n for i in range(n)]
        
        # 单调栈
        stack = []
        for i,num in enumerate(nums):
            while stack and prime_score[nums[stack[-1]]] < prime_score[num]:
                right[stack.pop()] = i
            if stack:
                left[i] = stack[-1]
            stack.append(i)
        
        # 快速幂
        res = 1
        for i, num, l, r in sorted(zip(range(n), nums, left, right), key=lambda z:-z[1]):
            count = (i - l) * (r - i)
            if count >= k:
                res = res * pow(num, k, MOD) % MOD
                break
            res = res * pow(num, count, MOD) % MOD
            k -= count
        return res
```

