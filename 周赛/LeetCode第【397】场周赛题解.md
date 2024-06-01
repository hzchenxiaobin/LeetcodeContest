###### **本文主要解析LeetCode在2024年5月12日10:30组织的第【398】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-397)**。**

---

### 题目一、[两个字符串的排列差](https://leetcode.cn/contest/weekly-contest-397/problems/permutation-difference-between-two-strings/)【简单】

#### 题目描述

给你两个字符串 `s` 和 `t`，每个字符串中的字符都不重复，且 `t` 是 `s` 的一个排列。

**排列差** 定义为 `s` 和 `t` 中每个字符在两个字符串中位置的绝对差值之和。

返回 `s` 和 `t` 之间的 **排列差** 。

 

**示例 1：**

**输入：**s = "abc", t = "bac"

**输出：**2

**解释：**

对于 `s = "abc"` 和 `t = "bac"`，排列差是：

- `"a"` 在 `s` 中的位置与在 `t` 中的位置之差的绝对值。
- `"b"` 在 `s` 中的位置与在 `t` 中的位置之差的绝对值。
- `"c"` 在 `s` 中的位置与在 `t` 中的位置之差的绝对值。

即，`s` 和 `t` 的排列差等于 `|0 - 1| + |2 - 2| + |1 - 0| = 2`。

**示例 2：**

**输入：**s = "abcde", t = "edbac"

**输出：**12

**解释：** `s` 和 `t` 的排列差等于 `|0 - 3| + |1 - 2| + |2 - 4| + |3 - 1| + |4 - 0| = 12`。

 

**提示：**

- `1 <= s.length <= 26`
- 每个字符在 `s` 中最多出现一次。
- `t` 是 `s` 的一个排列。
- `s` 仅由小写英文字母组成。

#### 分析

用两个map分别记录每个字符和位置，然后相同的相减即可。

#### 代码

```python
class Solution:
    def findPermutationDifference(self, s: str, t: str) -> int:
        s_m = {c:i for i, c in enumerate(s)}
        t_m = {c:i for i, c in enumerate(t)}
        return sum([abs(s_m[c] - t_m[c]) for c in s])    
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

