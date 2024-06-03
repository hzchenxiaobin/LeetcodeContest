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

### 题目二、[从魔法师身上吸取的最大能量](https://leetcode.cn/contest/weekly-contest-397/problems/taking-maximum-energy-from-the-mystic-dungeon/)【中等】

#### 题目描述

在神秘的地牢中，`n` 个魔法师站成一排。每个魔法师都拥有一个属性，这个属性可以给你提供能量。有些魔法师可能会给你负能量，即从你身上吸取能量。

你被施加了一种诅咒，当你从魔法师 `i` 处吸收能量后，你将被立即传送到魔法师 `(i + k)` 处。这一过程将重复进行，直到你到达一个不存在 `(i + k)` 的魔法师为止。

换句话说，你将选择一个起点，然后以 `k` 为间隔跳跃，直到到达魔法师序列的末端，**在过程中吸收所有的能量**。

给定一个数组 `energy` 和一个整数`k`，返回你能获得的 **最大** 能量。

 

**示例 1：**

**输入：** energy = [5,2,-10,-5,1], k = 3

**输出：** 3

**解释：**可以从魔法师 1 开始，吸收能量 2 + 1 = 3。

**示例 2：**

**输入：** energy = [-2,-3,-1], k = 2

**输出：** -1

**解释：**可以从魔法师 2 开始，吸收能量 -1。

 

**提示：**

- `1 <= energy.length <= 10^5`
- `-1000 <= energy[i] <= 1000`
- `1 <= k <= energy.length - 1`



#### 分析

可以将数组拆成k个子数组，从尾部往前遍历，取遍历过程中的最大值即可。



#### 代码

```Python
class Solution:
    def maximumEnergy(self, energy: List[int], k: int) -> int:        
        res = -inf
        n = len(energy)
        
        for i in range(n - 1, n - k - 1, -1):
            p = 0
            for j in range(i, -1, -k):
                p += energy[j]
                res = max(res, p)
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

