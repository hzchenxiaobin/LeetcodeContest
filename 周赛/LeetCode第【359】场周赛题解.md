###### **本文主要解析LeetCode在2023年8月20日10:30组织的第【359】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-359)**。**

---

### 题目一、[判别首字母缩略词](https://leetcode.cn/contest/weekly-contest-359/problems/check-if-a-string-is-an-acronym-of-words/)【简单】

#### 题目描述

给你一个字符串数组 `words` 和一个字符串 `s` ，请你判断 `s` 是不是 `words` 的 **首字母缩略词** 。

如果可以按顺序串联 `words` 中每个字符串的第一个字符形成字符串 `s` ，则认为 `s` 是 `words` 的首字母缩略词。例如，`"ab"` 可以由 `["apple", "banana"]` 形成，但是无法从 `["bear", "aardvark"]` 形成。

如果 `s` 是 `words` 的首字母缩略词，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

```
输入：words = ["alice","bob","charlie"], s = "abc"
输出：true
解释：words 中 "alice"、"bob" 和 "charlie" 的第一个字符分别是 'a'、'b' 和 'c'。因此，s = "abc" 是首字母缩略词。 
```

**示例 2：**

```
输入：words = ["an","apple"], s = "a"
输出：false
解释：words 中 "an" 和 "apple" 的第一个字符分别是 'a' 和 'a'。
串联这些字符形成的首字母缩略词是 "aa" 。
因此，s = "a" 不是首字母缩略词。
```

**示例 3：**

```
输入：words = ["never","gonna","give","up","on","you"], s = "ngguoy"
输出：true
解释：串联数组 words 中每个字符串的第一个字符，得到字符串 "ngguoy" 。
因此，s = "ngguoy" 是首字母缩略词。 
```

 

**提示：**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 10`
- `1 <= s.length <= 100`
- `words[i]` 和 `s` 由小写英文字母组成

#### 分析

直接模拟即可

#### 代码

```python
class Solution:
    def isAcronym(self, words: List[str], s: str) -> bool:
        return s == "".join([w[0] for w in words])
```



------

### 题目二、[k-avoiding 数组的最小总和](https://leetcode.cn/contest/weekly-contest-359/problems/determine-the-minimum-sum-of-a-k-avoiding-array/)【中等】

#### 题目描述

给你两个整数 `n` 和 `k` 。

对于一个由 **不同** 正整数组成的数组，如果其中不存在任何求和等于 k 的不同元素对，则称其为 **k-avoiding** 数组。

返回长度为 `n` 的 **k-avoiding** 数组的可能的最小总和。

 

**示例 1：**

```
输入：n = 5, k = 4
输出：18
解释：设若 k-avoiding 数组为 [1,2,4,5,6] ，其元素总和为 18 。
可以证明不存在总和小于 18 的 k-avoiding 数组。
```

**示例 2：**

```
输入：n = 2, k = 6
输出：3
解释：可以构造数组 [1,2] ，其元素总和为 3 。
可以证明不存在总和小于 3 的 k-avoiding 数组。 
```

 

**提示：**

- `1 <= n, k <= 50`

#### 分析

 **k-avoiding** 数组的可能的最小总和的数组形式应该是[1,2,3,4...]，把和为target的数对去掉即可

#### 代码

```Python
class Solution:
    def minimumSum(self, n: int, k: int) -> int:
        s = set()
        i = 1
        while len(s) < n:
            if k - i not in s:
                s.add(i)
            i += 1
        return sum(s)
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

