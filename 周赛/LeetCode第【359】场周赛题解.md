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

### 题目三、[销售利润最大化](https://leetcode.cn/contest/weekly-contest-359/problems/maximize-the-profit-as-the-salesman/)【中等】

#### 题目描述

给你一个整数 `n` 表示数轴上的房屋数量，编号从 `0` 到 `n - 1` 。

另给你一个二维整数数组 `offers` ，其中 `offers[i] = [starti, endi, goldi]` 表示第 `i` 个买家想要以 `goldi` 枚金币的价格购买从 `starti` 到 `endi` 的所有房屋。

作为一名销售，你需要有策略地选择并销售房屋使自己的收入最大化。

返回你可以赚取的金币的最大数目。

**注意** 同一所房屋不能卖给不同的买家，并且允许保留一些房屋不进行出售。

 

**示例 1：**

```
输入：n = 5, offers = [[0,0,1],[0,2,2],[1,3,2]]
输出：3
解释：
有 5 所房屋，编号从 0 到 4 ，共有 3 个购买要约。
将位于 [0,0] 范围内的房屋以 1 金币的价格出售给第 1 位买家，并将位于 [1,3] 范围内的房屋以 2 金币的价格出售给第 3 位买家。
可以证明我们最多只能获得 3 枚金币。
```

**示例 2：**

```
输入：n = 5, offers = [[0,0,1],[0,2,10],[1,3,2]]
输出：10
解释：有 5 所房屋，编号从 0 到 4 ，共有 3 个购买要约。
将位于 [0,2] 范围内的房屋以 10 金币的价格出售给第 2 位买家。
可以证明我们最多只能获得 10 枚金币。
```

 

**提示：**

- `1 <= n <= 10^5`
- `1 <= offers.length <= 10^5`
- `offers[i].length == 3`
- `0 <= starti <= endi <= n - 1`
- `1 <= goldi <= 10^3`

#### 分析

顺序dp问题。

顺序遍历n，遍历到i时，dp数组中存的是到i为止最大的利润。

步骤如下：

1.对offers进行排序，以end作为排序的key，从小到大排序。

2.遍历n，对于遍历到的i：

​    a.dp[i] = dp[i-1]  -> 让dp[i]等于前面一个最大的利润，这个能保证当前值是最大利润。

​    b.dp[i] = max(dp[i], dp[start - 1] + gold)  -> 算上end <= i的所有offer的最大值。

3.返回最后一个值，即dp[-1]。



处理步骤中有dp[i-1]和dp[start-1]，所以为了统一处理，对start和end都做了加1处理，房屋的编号从1到n。

#### 代码

```python
class Solution:
    def maximizeTheProfit(self, n: int, offers: List[List[int]]) -> int:
        dp = [0 for i in range(n+1)]
        offers.sort(key=lambda x:x[1])
        idx = 0
        for i in range(1, n+1):
            dp[i] = dp[i-1]
            while idx < len(offers) and offers[idx][1] + 1<= i:
                offer = offers[idx]
                start,end,gold = offer[0] + 1, offer[1] + 1, offer[2]
                dp[end] = max(dp[start - 1] + gold, dp[end])
                idx += 1
        return dp[-1]
```

------

### 题目四、[找出最长等值子数组](https://leetcode.cn/contest/weekly-contest-359/problems/find-the-longest-equal-subarray/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 和一个整数 `k` 。

如果子数组中所有元素都相等，则认为子数组是一个 **等值子数组** 。注意，空数组是 **等值子数组** 。

从 `nums` 中删除最多 `k` 个元素后，返回可能的最长等值子数组的长度。

**子数组** 是数组中一个连续且可能为空的元素序列。

 

**示例 1：**

```
输入：nums = [1,3,2,3,1,3], k = 3
输出：3
解释：最优的方案是删除下标 2 和下标 4 的元素。
删除后，nums 等于 [1, 3, 3, 3] 。
最长等值子数组从 i = 1 开始到 j = 3 结束，长度等于 3 。
可以证明无法创建更长的等值子数组。
```

**示例 2：**

```
输入：nums = [1,1,2,2,1,1], k = 2
输出：4
解释：最优的方案是删除下标 2 和下标 3 的元素。 
删除后，nums 等于 [1, 1, 1, 1] 。 
数组自身就是等值子数组，长度等于 4 。 
可以证明无法创建更长的等值子数组。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= nums.length`
- `0 <= k <= nums.length`

#### 分析

滑动窗口（双指针）

1.取滑动窗口最左边的值nums[l]作为比较对象

2.如果窗口内的非nums[l]元素个数小于等于k，那么说明可以通过删除至多k个元素形成等值数组

3.如果窗口内的非nums[l]元素个数大于k，那么说明不能通过删除至多k个元素形成等值数组，需要将左边的指针向右移动一个位置。

4.反复执行以上步骤，取最大值。



特殊处理：由于最后的窗口内，最多元素个数的并不一定是最左边的元素，所以要遍历最后的窗口，取得最大值。

#### 代码

```python
class Solution:
    def longestEqualSubarray(self, nums: List[int], k: int) -> int:
        l = 0
        n = len(nums)
        map = dict()
        res = 0
        for r in range(n):
            map[nums[r]] = map.get(nums[r], 0) + 1
            while l < r and r + 1 - l - map[nums[l]] > k:
                map[nums[l]] = map[nums[l]] - 1
                l += 1
            res = max(res, map[nums[l]])
        res = max(res, max(map.values()))
        return res
```

