###### **本文主要解析LeetCode在2023年7月22日22:30组织的第【109】场双周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/biweekly-contest-109/)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/hzchenxiaobin/)**。**

---

### 题目一、[检查数组是否是好的](https://leetcode.cn/contest/biweekly-contest-109/problems/check-if-array-is-good/)【简单】

#### 题目描述

给你一个整数数组 `nums` ，如果它是数组 `base[n]` 的一个排列，我们称它是个 **好** 数组。

`base[n] = [1, 2, ..., n - 1, n, n]` （换句话说，它是一个长度为 `n + 1` 且包含 `1` 到 `n - 1` 恰好各一次，包含 `n` 两次的一个数组）。比方说，`base[1] = [1, 1]` ，`base[3] = [1, 2, 3, 3]` 。

如果数组是一个好数组，请你返回 `true` ，否则返回 `false` 。

**注意：**数组的排列是这些数字按任意顺序排布后重新得到的数组。

 

**示例 1：**

```
输入：nums = [2, 1, 3]
输出：false
解释：因为数组的最大元素是 3 ，唯一可以构成这个数组的 base[n] 对应的 n = 3 。但是 base[3] 有 4 个元素，但数组 nums 只有 3 个元素，所以无法得到 base[3] = [1, 2, 3, 3] 的排列，所以答案为 false 。
```

**示例 2：**

```
输入：nums = [1, 3, 3, 2]
输出：true
解释：因为数组的最大元素是 3 ，唯一可以构成这个数组的 base[n] 对应的 n = 3 ，可以看出数组是 base[3] = [1, 2, 3, 3] 的一个排列（交换 nums 中第二个和第四个元素）。所以答案为 true 。
```

**示例 3：**

```
输入：nums = [1, 1]
输出：true
解释：因为数组的最大元素是 1 ，唯一可以构成这个数组的 base[n] 对应的 n = 1，可以看出数组是 base[1] = [1, 1] 的一个排列。所以答案为 true 。
```

**示例 4：**

```
输入：nums = [3, 4, 4, 1, 2, 1]
输出：false
解释：因为数组的最大元素是 4 ，唯一可以构成这个数组的 base[n] 对应的 n = 4 。但是 base[n] 有 5 个元素而 nums 有 6 个元素。所以答案为 false 。
```

 

**提示：**

- `1 <= nums.length <= 100`
- `1 <= num[i] <= 200`

#### 分析

对数组排序后按照题意模拟即可

#### 代码

```python
class Solution:
    def isGood(self, nums: List[int]) -> bool:
        nums.sort()
        n = len(nums)
        for i in range(n):
            # 最后一个为n-1
            if i == n - 1:
                return nums[i] == n - 1
            # 不是最后一个时为 i+1
            if nums[i] != i+1:
                return False
```



------

### 题目二、[将字符串中的元音字母排序](https://leetcode.cn/contest/biweekly-contest-109/problems/sort-vowels-in-a-string/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的字符串 `s` ，将 `s` 中的元素重新 **排列** 得到新的字符串 `t` ，它满足：

- 所有辅音字母都在原来的位置上。更正式的，如果满足 `0 <= i < s.length` 的下标 `i` 处的 `s[i]` 是个辅音字母，那么 `t[i] = s[i]` 。
- 元音字母都必须以他们的 **ASCII** 值按 **非递减** 顺序排列。更正式的，对于满足 `0 <= i < j < s.length` 的下标 `i` 和 `j` ，如果 `s[i]` 和 `s[j]` 都是元音字母，那么 `t[i]` 的 ASCII 值不能大于 `t[j]` 的 ASCII 值。

请你返回结果字母串。

元音字母为 `'a'` ，`'e'` ，`'i'` ，`'o'` 和 `'u'` ，它们可能是小写字母也可能是大写字母，辅音字母是除了这 5 个字母以外的所有字母。

 

**示例 1：**

```
输入：s = "lEetcOde"
输出："lEOtcede"
解释：'E' ，'O' 和 'e' 是 s 中的元音字母，'l' ，'t' ，'c' 和 'd' 是所有的辅音。将元音字母按照 ASCII 值排序，辅音字母留在原地。
```

**示例 2：**

```
输入：s = "lYmpH"
输出："lYmpH"
解释：s 中没有元音字母（s 中都为辅音字母），所以我们返回 "lYmpH" 。
```

 

**提示：**

- `1 <= s.length <= 10^5`
- `s` 只包含英语字母表中的 **大写** 和 **小写** 字母。

#### 分析

单独将字符串中的元音字母提取出来，排序后再重新填回原先元音字母的位置

#### 代码

```Python
class Solution:
    def sortVowels(self, s: str) -> str:
        s_set = set("aeiuoAEIUO")
        n = len(s)
        tmp = sorted([c for c in s if c in s_set])[::-1]
                      
        s = list(s)
        for i,c in enumerate(s):
            if c in s_set:
                s[i] = tmp.pop()
        return ''.join(s)
```

------

### 题目三、[访问数组中的位置使分数最大](https://leetcode.cn/contest/biweekly-contest-109/problems/visit-array-positions-to-maximize-score/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 和一个正整数 `x` 。

你 **一开始** 在数组的位置 `0` 处，你可以按照下述规则访问数组中的其他位置：

- 如果你当前在位置 `i` ，那么你可以移动到满足 `i < j` 的 **任意** 位置 `j` 。
- 对于你访问的位置 `i` ，你可以获得分数 `nums[i]` 。
- 如果你从位置 `i` 移动到位置 `j` 且 `nums[i]` 和 `nums[j]` 的 **奇偶性** 不同，那么你将失去分数 `x` 。

请你返回你能得到的 **最大** 得分之和。

**注意** ，你一开始的分数为 `nums[0]` 。

 

**示例 1：**

```
输入：nums = [2,3,6,1,9,2], x = 5
输出：13
解释：我们可以按顺序访问数组中的位置：0 -> 2 -> 3 -> 4 。
对应位置的值为 2 ，6 ，1 和 9 。因为 6 和 1 的奇偶性不同，所以下标从 2 -> 3 让你失去 x = 5 分。
总得分为：2 + 6 + 1 + 9 - 5 = 13 。
```

**示例 2：**

```
输入：nums = [2,4,6,8], x = 3
输出：20
解释：数组中的所有元素奇偶性都一样，所以我们可以将每个元素都访问一次，而且不会失去任何分数。
总得分为：2 + 4 + 6 + 8 = 20 。
```

 

**提示：**

- `2 <= nums.length <= 10^5`
- `1 <= nums[i], x <= 10^6`

#### 分析

使用odd和even表示在第i个数之前的奇数最大值和偶数最大值，那么在第i个数时：

1.若第i个数为奇数，则：

- 从偶数移动过来：even + nums[i] - x
- 从奇数移动过来：odd + nums[i]

所以最终的奇数最大值odd = max(odd + nums[i],  even + nums[i] - x) = max(odd, even - x) + nums[i]

2.若第i个数为偶数时，则：

- 从偶数移动过来：even + nums[i]
- 从奇数移动过来：odd + nums[i] - x

所以最终的奇数最大值even = max(even + nums[i],  odd + nums[i] - x) = max(even, odd - x) + nums[i]

最后返回max(even, odd)

#### 代码

```python
class Solution:
    def maxScore(self, nums: List[int], x: int) -> int:
        even = odd = -10**6
        if nums[0] & 1:
            odd = nums[0]
        else:
            even = nums[0]
            
        for num in nums[1:]:
            if num & 1:
                odd = max(odd, even - x) + num
            else:
                even = max(even, odd - x) + num
        return max(odd, even)
```

------

### 题目四、【中等】

#### 题目描述



#### 分析



#### 代码

```python

```

