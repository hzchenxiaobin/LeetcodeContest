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

