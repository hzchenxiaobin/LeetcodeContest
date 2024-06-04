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

