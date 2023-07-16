###### **本文主要解析LeetCode在2023年7月16日10:30组织的第【354】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-354)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/hzchenxiaobin/)**。**

---

### 题目一、[特殊元素平方和](https://leetcode.cn/contest/weekly-contest-354/problems/sum-of-squares-of-special-elements/)【简单】

#### 题目描述

给你一个下标从 **1** 开始、长度为 `n` 的整数数组 `nums` 。

对 `nums` 中的元素 `nums[i]` 而言，如果 `n` 能够被 `i` 整除，即 `n % i == 0` ，则认为 `num[i]` 是一个 **特殊元素** 。

返回 `nums` 中所有 **特殊元素** 的 **平方和** 。

 

**示例 1：**

```
输入：nums = [1,2,3,4]
输出：21
解释：nums 中共有 3 个特殊元素：nums[1] ，因为 4 被 1 整除；nums[2] ，因为 4 被 2 整除；以及 nums[4] ，因为 4 被 4 整除。 
因此，nums 中所有元素的平方和等于 nums[1] * nums[1] + nums[2] * nums[2] + nums[4] * nums[4] = 1 * 1 + 2 * 2 + 4 * 4 = 21 。  
```

**示例 2：**

```
输入：nums = [2,7,1,19,18,3]
输出：63
解释：nums 中共有 4 个特殊元素：nums[1] ，因为 6 被 1 整除；nums[2] ，因为 6 被 2 整除；nums[3] ，因为 6 被 3 整除；以及 nums[6] ，因为 6 被 6 整除。 
因此，nums 中所有元素的平方和等于 nums[1] * nums[1] + nums[2] * nums[2] + nums[3] * nums[3] + nums[6] * nums[6] = 2 * 2 + 7 * 7 + 1 * 1 + 3 * 3 = 63 。 
```

 

**提示：**

- `1 <= nums.length == n <= 50`
- `1 <= nums[i] <= 50`

#### 分析

简单题，按照题意模拟即可

#### 代码

```python
class Solution:
    def sumOfSquares(self, nums: List[int]) -> int:
        res = 0
        n = len(nums)
        for i,num in enumerate(nums):
            if n % (i+1) == 0:
                res += num * num
        return res
```



------

### 题目二、[数组的最大美丽值](https://leetcode.cn/contest/weekly-contest-354/problems/maximum-beauty-of-an-array-after-applying-operation/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 和一个 **非负** 整数 `k` 。

在一步操作中，你可以执行下述指令：

- 在范围 `[0, nums.length - 1]` 中选择一个 **此前没有选过** 的下标 `i` 。
- 将 `nums[i]` 替换为范围 `[nums[i] - k, nums[i] + k]` 内的任一整数。

数组的 **美丽值** 定义为数组中由相等元素组成的最长子序列的长度。

对数组 `nums` 执行上述操作任意次后，返回数组可能取得的 **最大** 美丽值。

**注意：**你 **只** 能对每个下标执行 **一次** 此操作。

数组的 **子序列** 定义是：经由原数组删除一些元素（也可能不删除）得到的一个新数组，且在此过程中剩余元素的顺序不发生改变。

 

**示例 1：**

```
输入：nums = [4,6,1,2], k = 2
输出：3
解释：在这个示例中，我们执行下述操作：
- 选择下标 1 ，将其替换为 4（从范围 [4,8] 中选出），此时 nums = [4,4,1,2] 。
- 选择下标 3 ，将其替换为 4（从范围 [0,4] 中选出），此时 nums = [4,4,1,4] 。
执行上述操作后，数组的美丽值是 3（子序列由下标 0 、1 、3 对应的元素组成）。
可以证明 3 是我们可以得到的由相等元素组成的最长子序列长度。
```

**示例 2：**

```
输入：nums = [1,1,1,1], k = 10
输出：4
解释：在这个示例中，我们无需执行任何操作。
数组 nums 的美丽值是 4（整个数组）。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `0 <= nums[i], k <= 10^5`

#### 分析

排序后滑动窗口

如果窗口的最右边元素减最左边元素小于等于 2 * k，则能够将整个窗口内的元素按照题意替换为同一个值（不需要知道具体是哪一个值）。

#### 代码

```Python
class Solution:
    def maximumBeauty(self, nums: List[int], k: int) -> int:
        nums.sort()
        l,r = 0, 0
        res = 1
        for r in range(len(nums)):
            while nums[r] - nums[l] > 2 * k:
                l += 1
            res = max(res, r - l + 1)
        return res
```

------

### 题目三、[合法分割的最小下标](https://leetcode.cn/contest/weekly-contest-354/problems/minimum-index-of-a-valid-split/)【中等】

#### 题目描述

如果元素 `x` 在长度为 `m` 的整数数组 `arr` 中满足 `freq(x) * 2 > m` ，那么我们称 `x` 是 **支配元素** 。其中 `freq(x)` 是 `x` 在数组 `arr` 中出现的次数。注意，根据这个定义，数组 `arr` **最多** 只会有 **一个** 支配元素。

给你一个下标从 **0** 开始长度为 `n` 的整数数组 `nums` ，数据保证它含有一个支配元素。

你需要在下标 `i` 处将 `nums` 分割成两个数组 `nums[0, ..., i]` 和 `nums[i + 1, ..., n - 1]` ，如果一个分割满足以下条件，我们称它是 **合法** 的：

- `0 <= i < n - 1`
- `nums[0, ..., i]` 和 `nums[i + 1, ..., n - 1]` 的支配元素相同。

这里， `nums[i, ..., j]` 表示 `nums` 的一个子数组，它开始于下标 `i` ，结束于下标 `j` ，两个端点都包含在子数组内。特别地，如果 `j < i` ，那么 `nums[i, ..., j]` 表示一个空数组。

请你返回一个 **合法分割** 的 **最小** 下标。如果合法分割不存在，返回 `-1` 。

 

**示例 1：**

```
输入：nums = [1,2,2,2]
输出：2
解释：我们将数组在下标 2 处分割，得到 [1,2,2] 和 [2] 。
数组 [1,2,2] 中，元素 2 是支配元素，因为它在数组中出现了 2 次，且 2 * 2 > 3 。
数组 [2] 中，元素 2 是支配元素，因为它在数组中出现了 1 次，且 1 * 2 > 1 。
两个数组 [1,2,2] 和 [2] 都有与 nums 一样的支配元素，所以这是一个合法分割。
下标 2 是合法分割中的最小下标。
```

**示例 2：**

```
输入：nums = [2,1,3,1,1,1,7,1,2,1]
输出：4
解释：我们将数组在下标 4 处分割，得到 [2,1,3,1,1] 和 [1,7,1,2,1] 。
数组 [2,1,3,1,1] 中，元素 1 是支配元素，因为它在数组中出现了 3 次，且 3 * 2 > 5 。
数组 [1,7,1,2,1] 中，元素 1 是支配元素，因为它在数组中出现了 3 次，且 3 * 2 > 5 。
两个数组 [2,1,3,1,1] 和 [1,7,1,2,1] 都有与 nums 一样的支配元素，所以这是一个合法分割。
下标 4 是所有合法分割中的最小下标。
```

**示例 3：**

```
输入：nums = [3,3,3,3,7,2,2]
输出：-1
解释：没有合法分割。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^9`
- `nums` 有且只有一个支配元素。

#### 分析

1.找出支配元素target和支配元素出现的个数target_count

2.遍历数组，统计支配元素在第一个子数组中的出现次数count，则第二个数组中支配元素出现的次数则是target_count - count

3.判断支配元素是否是第一个子数组中的支配元素：count * 2 > i + 1

4.判断支配元素是否是第二个子数组中的支配元素：(target_count - count) * 2 > (m - i - 1)

#### 代码

```python
class Solution:
    def minimumIndex(self, nums: List[int]) -> int:
        # 找出支配元素和支配元素的个数
        m = len(nums)
        counter = Counter(nums)
        target, target_count = [(k,v) for k, v in counter.items() if v*2 > m][0]
                
        count = 0
        for i in range(m):
            if nums[i] == target:
                count += 1
            #1.target是第一个子数组的支配元素：count * 2 > i + 1
            #2.target是第二个子数组的支配元素：(target_count - count) * 2 > (m - i - 1)
            if count * 2 > i + 1 and (target_count - count) * 2 > (m - i - 1):
                return i
        return -1
```

------

### 题目四、[最长合法子字符串的长度](https://leetcode.cn/contest/weekly-contest-354/problems/length-of-the-longest-valid-substring/)【困难】

#### 题目描述

给你一个字符串 `word` 和一个字符串数组 `forbidden` 。

如果一个字符串不包含 `forbidden` 中的任何字符串，我们称这个字符串是 **合法** 的。

请你返回字符串 `word` 的一个 **最长合法子字符串** 的长度。

**子字符串** 指的是一个字符串中一段连续的字符，它可以为空。

 

**示例 1：**

```
输入：word = "cbaaaabc", forbidden = ["aaa","cb"]
输出：4
解释：总共有 9 个合法子字符串："c" ，"b" ，"a" ，"ba" ，"aa" ，"bc" ，"baa" ，"aab" 和 "aabc" 。最长合法子字符串的长度为 4 。
其他子字符串都要么包含 "aaa" ，要么包含 "cb" 。
```

**示例 2：**

```
输入：word = "leetcode", forbidden = ["de","le","e"]
输出：4
解释：总共有 11 个合法子字符串："l" ，"t" ，"c" ，"o" ，"d" ，"tc" ，"co" ，"od" ，"tco" ，"cod" 和 "tcod" 。最长合法子字符串的长度为 4 。
所有其他子字符串都至少包含 "de" ，"le" 和 "e" 之一。
```

 

**提示：**

- `1 <= word.length <= 10^5`
- `word` 只包含小写英文字母。
- `1 <= forbidden.length <= 10^5`
- `1 <= forbidden[i].length <= 10`
- `forbidden[i]` 只包含小写英文字母。

#### 分析

滑动窗口

最重要的性质：`1 <= forbidden[i].length <= 10`，可以从短到长遍历窗口的右边字符串，如果该字符串存在于forbidden处，则将left增加到字符串首字母的右侧第一个字母的索引处。

比如：

输入：word = "abcd",  forbidden = ["abc", "bc"]

![](https://github.com/hzchenxiaobin/LeetcodeContest/blob/master/resource/pic/354/354_1.png?raw=true)

#### 代码

```python
class Solution:
    def longestValidSubstring(self, word: str, forbidden: List[str]) -> int:
        n = len(word)
        forbidden_set = set(forbidden)
        left, right = 0,0
        res = 0
        for right in range(n):
            for length in range(1, min(right - left + 2, 11)):
                if word[right - length + 1:right+1] in forbidden_set:
                    left = right - length + 2
                    break
            res = max(res, right - left + 1)
                
        return res
```

