###### **本文主要解析LeetCode在2024年5月5日10:30组织的第【396】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-396)**。**

---

### 题目一、[有效单词](https://leetcode.cn/contest/weekly-contest-396/problems/valid-word/)【简单】

#### 题目描述

**有效单词** 需要满足以下几个条件：

- **至少** 包含 3 个字符。
- 由数字 0-9 和英文大小写字母组成。（不必包含所有这类字符。）
- **至少** 包含一个 **元音字母** 。
- **至少** 包含一个 **辅音字母** 。

给你一个字符串 `word` 。如果 `word` 是一个有效单词，则返回 `true` ，否则返回 `false` 。

**注意：**

- `'a'`、`'e'`、`'i'`、`'o'`、`'u'` 及其大写形式都属于 **元音字母** 。
- 英文中的 **辅音字母** 是指那些除元音字母之外的字母。

 

**示例 1：**

**输入：**word = "234Adas"

**输出：**true

**解释：**

这个单词满足所有条件。

**示例 2：**

**输入：**word = "b3"

**输出：**false

**解释：**

这个单词的长度少于 3 且没有包含元音字母。

**示例 3：**

**输入：**word = "a3$e"

**输出：**false

**解释：**

这个单词包含了 `'$'` 字符且没有包含辅音字母。

 

**提示：**

- `1 <= word.length <= 20`
- `word` 由英文大写和小写字母、数字、`'@'`、`'#'` 和 `'$'` 组成。

#### 分析

按照题意模拟即可，这里判断条件2的时候可以反过来思考，字符中只包含英文字母、数字和三个特殊字符，只要判断没有特殊字符就是满足条件2。

#### 代码

```python
class Solution:
    def isValid(self, word: str) -> bool:
        if len(word) < 3:
            return False
        vowel, consonant = False
        for c in word:
            if c == '@' or c == '#' or c == '$':
                return False
            if c >= '0' and c <= '9':
                continue
            if c.lower() in 'aeiou':
                vowel = True
            else:
                consonant = True
        return vowel and consonant
```



------

### 题目二、[K 周期字符串需要的最少操作次数](https://leetcode.cn/contest/weekly-contest-396/problems/minimum-number-of-operations-to-make-word-k-periodic/)【中等】

#### 题目描述

给你一个长度为 `n` 的字符串 `word` 和一个整数 `k` ，其中 `k` 是 `n` 的因数。

在一次操作中，你可以选择任意两个下标 `i` 和 `j`，其中 `0 <= i, j < n` ，且这两个下标都可以被 `k` 整除，然后用从 `j` 开始的长度为 `k` 的子串替换从 `i` 开始的长度为 `k` 的子串。也就是说，将子串 `word[i..i + k - 1]` 替换为子串 `word[j..j + k - 1]` 。

返回使 `word` 成为 **K 周期字符串** 所需的 **最少** 操作次数。

如果存在某个长度为 `k` 的字符串 `s`，使得 `word` 可以表示为任意次数连接 `s` ，则称字符串 `word` 是 **K 周期字符串** 。例如，如果 `word == "ababab"`，那么 `word` 就是 `s = "ab"` 时的 2 周期字符串 。

 

**示例 1：**

**输入：**word = "leetcodeleet", k = 4

**输出：**1

**解释：**可以选择 i = 4 和 j = 0 获得一个 4 周期字符串。这次操作后，word 变为 "leetleetleet" 。

**示例 2：**

**输入：**word = "leetcoleet", k = 2

**输出：**3

**解释：**可以执行以下操作获得一个 2 周期字符串。

| i    | j    | word       |
| ---- | ---- | ---------- |
| 0    | 2    | etetcoleet |
| 4    | 0    | etetetleet |
| 6    | 0    | etetetetet |

 

**提示：**

- `1 <= n == word.length <= 10^5`
- `1 <= k <= word.length`
- `k` 能整除 `word.length` 。
- `word` 仅由小写英文字母组成。



#### 分析

统计从0开始步长为k的字符串的个数，取最大的个数即为最终需要转换成的字符串。



#### 代码

```Python
class Solution:
    def minimumOperationsToMakeKPeriodic(self, word: str, k: int) -> int:
        n = len(word)
        counter = Counter([word[i:i+k] for i in range(0, n, k)])
        res = n
        for _, count in counter.items():
            res = min(n // k - count, res)
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

