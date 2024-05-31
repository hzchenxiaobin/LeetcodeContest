###### **本文主要解析LeetCode在2024年5月26日10:30组织的第【399】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-399)**。**

---

### 题目一、[优质数对的总数 I](https://leetcode.cn/contest/weekly-contest-399/problems/find-the-number-of-good-pairs-i/)【简单】

#### 题目描述

给你两个整数数组 `nums1` 和 `nums2`，长度分别为 `n` 和 `m`。同时给你一个**正整数** `k`。

如果 `nums1[i]` 可以被 `nums2[j] * k` 整除，则称数对 `(i, j)` 为 **优质数对**（`0 <= i <= n - 1`, `0 <= j <= m - 1`）。

返回 **优质数对** 的总数。

 

**示例 1：**

**输入：**nums1 = [1,3,4], nums2 = [1,3,4], k = 1

**输出：**5

**解释：**

5个优质数对分别是 `(0, 0)`, `(1, 0)`, `(1, 1)`, `(2, 0)`, 和 `(2, 2)`。

**示例 2：**

**输入：**nums1 = [1,2,4,12], nums2 = [2,4], k = 3

**输出：**2

**解释：**

2个优质数对分别是 `(3, 0)` 和 `(3, 1)`。

 

**提示：**

- `1 <= n, m <= 50`
- `1 <= nums1[i], nums2[j] <= 50`
- `1 <= k <= 50`

#### 分析

简单题，按照题意模拟即可

#### 代码

```python
class Solution:
    def numberOfPairs(self, nums1: List[int], nums2: List[int], k: int) -> int:
        res = 0
        for num2 in nums2:
            for num1 in nums1:
                res += num1 % (k * num2) == 0
        return res
```



------

### 题目二、[压缩字符串 III](https://leetcode.cn/contest/weekly-contest-399/problems/string-compression-iii/)【中等】

#### 题目描述


 显示英文描述

 

[我的提交](https://leetcode.cn/contest/weekly-contest-399/problems/string-compression-iii/submissions/)[返回竞赛](https://leetcode.cn/contest/weekly-contest-399/)

- **通过的用户数**2631
- **尝试过的用户数**2743
- **用户总通过次数**2673
- **用户总提交次数**4844
- **题目难度****Medium**

给你一个字符串 `word`，请你使用以下算法进行压缩：

- 从空字符串

   

  ```
  comp
  ```

   

  开始。当

   

  ```
  word
  ```

   

  不为空

   

  时，执行以下操作：

  - 移除 `word` 的最长单字符前缀，该前缀由单一字符 `c` 重复多次组成，且该前缀长度 **最多** 为 9 。
  - 将前缀的长度和字符 `c` 追加到 `comp` 。

返回字符串 `comp` 。

 

 

**示例 1：**

**输入：**word = "abcde"

**输出：**"1a1b1c1d1e"

**解释：**

初始时，`comp = ""` 。进行 5 次操作，每次操作分别选择 `"a"`、`"b"`、`"c"`、`"d"` 和 `"e"` 作为前缀。

对每个前缀，将 `"1"` 和对应的字符追加到 `comp`。

**示例 2：**

**输入：**word = "aaaaaaaaaaaaaabb"

**输出：**"9a5a2b"

**解释：**

初始时，`comp = ""`。进行 3 次操作，每次操作分别选择 `"aaaaaaaaa"`、`"aaaaa"` 和 `"bb"` 作为前缀。

- 对于前缀 `"aaaaaaaaa"`，将 `"9"` 和 `"a"` 追加到 `comp`。
- 对于前缀 `"aaaaa"`，将 `"5"` 和 `"a"` 追加到 `comp`。
- 对于前缀 `"bb"`，将 `"2"` 和 `"b"` 追加到 `comp`。

 

**提示：**

- `1 <= word.length <= 2 * 10^5`
- `word` 仅由小写英文字母组成。



#### 分析

按题意模拟即可

使用一个索引i记录当前的位置，索引从0开始，并且记录当前的字符c，如果str[i] == c,则计数器count加1，然后索引往后移动一个位置。直到字符不相等或者count>=9.

#### 代码

```Python
class Solution:
    def compressedString(self, word: str) -> str:
        n = len(word)
        index = 0
        res = ""
        while index < n:
            c = word[index]
            count = 0
            while index < n and word[index] == c and count < 9:
                index += 1
                count += 1
            res += str(count)
            res += c
        return res
```

------

### 题目三、[优质数对的总数 II](https://leetcode.cn/contest/weekly-contest-399/problems/find-the-number-of-good-pairs-ii/)【中等】

#### 题目描述

给你两个整数数组 `nums1` 和 `nums2`，长度分别为 `n` 和 `m`。同时给你一个**正整数** `k`。

如果 `nums1[i]` 可以被 `nums2[j] * k` 整除，则称数对 `(i, j)` 为 **优质数对**（`0 <= i <= n - 1`, `0 <= j <= m - 1`）。

返回 **优质数对** 的总数。

 

**示例 1：**

**输入：**nums1 = [1,3,4], nums2 = [1,3,4], k = 1

**输出：**5

**解释：**

5个优质数对分别是 `(0, 0)`, `(1, 0)`, `(1, 1)`, `(2, 0)`, 和 `(2, 2)`。

**示例 2：**

**输入：**nums1 = [1,2,4,12], nums2 = [2,4], k = 3

**输出：**2

**解释：**

2个优质数对分别是 `(3, 0)` 和 `(3, 1)`。

 

**提示：**

- `1 <= n, m <= 10^5`
- `1 <= nums1[i], nums2[j] <= 10^6`
- `1 <= k <= 10^3`

#### 分析



#### 代码

```python
class Solution:
    def numberOfPairs(self, nums1: List[int], nums2: List[int], k: int) -> int:
        counter = Counter(nums2)
        res = 0
        
        for num in nums1:
            if num % k:
                continue
            num //= k
            
            for i in range(1, isqrt(num) + 1):
                if num % i:
                    continue
                res += counter[i]
                if num // i > isqrt(num):
                    res += counter[num // i]
        return res
```

------

### 题目四、【困难】

#### 题目描述



#### 分析



#### 代码

```python

```

