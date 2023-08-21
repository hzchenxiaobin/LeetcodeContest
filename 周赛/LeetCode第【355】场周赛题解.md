###### **本文主要解析LeetCode在2023年7月23日10:30组织的第【355】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-355)**。**

---

### 题目一、[按分隔符拆分字符串](https://leetcode.cn/contest/weekly-contest-355/problems/split-strings-by-separator/)【简单】

#### 题目描述

给你一个字符串数组 `words` 和一个字符 `separator` ，请你按 `separator` 拆分 `words` 中的每个字符串。

返回一个由拆分后的新字符串组成的字符串数组，**不包括空字符串** 。

**注意**

- `separator` 用于决定拆分发生的位置，但它不包含在结果字符串中。
- 拆分可能形成两个以上的字符串。
- 结果字符串必须保持初始相同的先后顺序。

 

**示例 1：**

```
输入：words = ["one.two.three","four.five","six"], separator = "."
输出：["one","two","three","four","five","six"]
解释：在本示例中，我们进行下述拆分：

"one.two.three" 拆分为 "one", "two", "three"
"four.five" 拆分为 "four", "five"
"six" 拆分为 "six" 

因此，结果数组为 ["one","two","three","four","five","six"] 。
```

**示例 2：**

```
输入：words = ["$easy$","$problem$"], separator = "$"
输出：["easy","problem"]
解释：在本示例中，我们进行下述拆分：

"$easy$" 拆分为 "easy"（不包括空字符串）
"$problem$" 拆分为 "problem"（不包括空字符串）

因此，结果数组为 ["easy","problem"] 。
```

**示例 3：**

```
输入：words = ["|||"], separator = "|"
输出：[]
解释：在本示例中，"|||" 的拆分结果将只包含一些空字符串，所以我们返回一个空数组 [] 。 
```

 

**提示：**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 20`
- `words[i]` 中的字符要么是小写英文字母，要么就是字符串 `".,|$#@"` 中的字符（不包括引号）
- `separator` 是字符串 `".,|$#@"` 中的某个字符（不包括引号）

#### 分析

按题意模拟拆分即可。

#### 代码

```python
class Solution:
    def splitWordsBySeparator(self, words: List[str], separator: str) -> List[str]:
        res = []
        for word in words:
            res += [x for x in word.split(separator) if x]
        return res
```



------

### 题目二、[合并后数组中的最大元素](https://leetcode.cn/contest/weekly-contest-355/problems/largest-element-in-an-array-after-merge-operations/)【中等】

#### 题目描述

给你一个下标从 **0** 开始、由正整数组成的数组 `nums` 。

你可以在数组上执行下述操作 **任意** 次：

- 选中一个同时满足 `0 <= i < nums.length - 1` 和 `nums[i] <= nums[i + 1]` 的整数 `i` 。将元素 `nums[i + 1]` 替换为 `nums[i] + nums[i + 1]` ，并从数组中删除元素 `nums[i]` 。

返回你可以从最终数组中获得的 **最大** 元素的值。

 

**示例 1：**

```
输入：nums = [2,3,7,9,3]
输出：21
解释：我们可以在数组上执行下述操作：
- 选中 i = 0 ，得到数组 nums = [5,7,9,3] 。
- 选中 i = 1 ，得到数组 nums = [5,16,3] 。
- 选中 i = 0 ，得到数组 nums = [21,3] 。
最终数组中的最大元素是 21 。可以证明我们无法获得更大的元素。
```

**示例 2：**

```
输入：nums = [5,3,3]
输出：11
解释：我们可以在数组上执行下述操作：
- 选中 i = 1 ，得到数组 nums = [5,6] 。
- 选中 i = 0 ，得到数组 nums = [11] 。
最终数组中只有一个元素，即 11 。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^6`

#### 分析

从后向前遍历，如果前一个元素大于当前元素则选择前一个元素，如果前一个元素小于等于当前元素则将当前元素加上前一个元素。

#### 代码

```Python
class Solution:
    def maxArrayValue(self, nums: List[int]) -> int:
        n = len(nums)
        res = 0
        for i in range(n-1, -1, -1):
            if nums[i] <= res:
                res += nums[i]
            else:
                res = nums[i]
        return res
```

------

### 题目三、[长度递增组的最大数目](https://leetcode.cn/contest/weekly-contest-355/problems/maximum-number-of-groups-with-increasing-length/)【中等】

#### 题目描述

给你一个下标从 **0** 开始、长度为 `n` 的数组 `usageLimits` 。

你的任务是使用从 `0` 到 `n - 1` 的数字创建若干组，并确保每个数字 `i` 在 **所有组** 中使用的次数总共不超过 `usageLimits[i]` 次。此外，还必须满足以下条件：

- 每个组必须由 **不同** 的数字组成，也就是说，单个组内不能存在重复的数字。
- 每个组（除了第一个）的长度必须 **严格大于** 前一个组。

在满足所有条件的情况下，以整数形式返回可以创建的最大组数。

 

**示例 1：**

```
输入：usageLimits = [1,2,5]
输出：3
解释：在这个示例中，我们可以使用 0 至多一次，使用 1 至多 2 次，使用 2 至多 5 次。
一种既能满足所有条件，又能创建最多组的方式是： 
组 1 包含数字 [2] 。
组 2 包含数字 [1,2] 。
组 3 包含数字 [0,1,2] 。 
可以证明能够创建的最大组数是 3 。 
所以，输出是 3 。 
```

**示例 2：**

```
输入：usageLimits = [2,1,2]
输出：2
解释：在这个示例中，我们可以使用 0 至多 2 次，使用 1 至多 1 次，使用 2 至多 2 次。
一种既能满足所有条件，又能创建最多组的方式是： 
组 1 包含数字 [0] 。 
组 2 包含数字 [1,2] 。
可以证明能够创建的最大组数是 2 。 
所以，输出是 2 。 
```

**示例 3：**

```
输入：usageLimits = [1,1]
输出：1
解释：在这个示例中，我们可以使用 0 和 1 至多 1 次。 
一种既能满足所有条件，又能创建最多组的方式是：
组 1 包含数字 [0] 。
可以证明能够创建的最大组数是 1 。 
所以，输出是 1 。 
```

 

**提示：**

- `1 <= usageLimits.length <= 10^5`
- `1 <= usageLimits[i] <= 10^9`

#### 分析



#### 代码

```python

```

------

### 题目四、[树中可以形成回文的路径数](https://leetcode.cn/contest/weekly-contest-355/problems/count-paths-that-can-form-a-palindrome-in-a-tree/)【困难】

#### 题目描述

给你一棵 **树**（即，一个连通、无向且无环的图），**根** 节点为 `0` ，由编号从 `0` 到 `n - 1` 的 `n` 个节点组成。这棵树用一个长度为 `n` 、下标从 **0** 开始的数组 `parent` 表示，其中 `parent[i]` 为节点 `i` 的父节点，由于节点 `0` 为根节点，所以 `parent[0] == -1` 。

另给你一个长度为 `n` 的字符串 `s` ，其中 `s[i]` 是分配给 `i` 和 `parent[i]` 之间的边的字符。`s[0]` 可以忽略。

找出满足 `u < v` ，且从 `u` 到 `v` 的路径上分配的字符可以 **重新排列** 形成 **回文** 的所有节点对 `(u, v)` ，并返回节点对的数目。

如果一个字符串正着读和反着读都相同，那么这个字符串就是一个 **回文** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2023/07/15/treedrawio-8drawio.png)

```
输入：parent = [-1,0,0,1,1,2], s = "acaabc"
输出：8
解释：符合题目要求的节点对分别是：
- (0,1)、(0,2)、(1,3)、(1,4) 和 (2,5) ，路径上只有一个字符，满足回文定义。
- (2,3)，路径上字符形成的字符串是 "aca" ，满足回文定义。
- (1,5)，路径上字符形成的字符串是 "cac" ，满足回文定义。
- (3,5)，路径上字符形成的字符串是 "acac" ，可以重排形成回文 "acca" 。
```

**示例 2：**

```
输入：parent = [-1,0,0,0,0], s = "aaaaa"
输出：10
解释：任何满足 u < v 的节点对 (u,v) 都符合题目要求。
```

 

**提示：**

- `n == parent.length == s.length`
- `1 <= n <= 105`
- 对于所有 `i >= 1` ，`0 <= parent[i] <= n - 1` 均成立
- `parent[0] == -1`
- `parent` 表示一棵有效的树
- `s` 仅由小写英文字母组成

#### 分析



#### 代码

```python

```

