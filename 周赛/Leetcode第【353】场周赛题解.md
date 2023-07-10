###### **本文主要解析LeetCode在2023年7月9日10：30组织的第【353】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-353)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/hzchenxiaobin/)**。**

---

### 题目一、[找出最大的可达成数字](https://leetcode.cn/contest/weekly-contest-353/problems/find-the-maximum-achievable-number/)【简单】

#### 题目描述

给你两个整数 `num` 和 `t` 。

如果整数 `x` 可以在执行下述操作不超过 `t` 次的情况下变为与 `num` 相等，则称其为 **可达成数字** ：

- 每次操作将 `x` 的值增加或减少 `1` ，同时可以选择将 `num` 的值增加或减少 `1` 。

返回所有可达成数字中的最大值。可以证明至少存在一个可达成数字。

 

**示例 1：**

```
输入：num = 4, t = 1
输出：6
解释：最大可达成数字是 x = 6 ，执行下述操作可以使其等于 num ：
- x 减少 1 ，同时 num 增加 1 。此时，x = 5 且 num = 5 。 
可以证明不存在大于 6 的可达成数字。
```

**示例 2：**

```
输入：num = 3, t = 2
输出：7
解释：最大的可达成数字是 x = 7 ，执行下述操作可以使其等于 num ：
- x 减少 1 ，同时 num 增加 1 。此时，x = 6 且 num = 4 。 
- x 减少 1 ，同时 num 增加 1 。此时，x = 5 且 num = 5 。 
可以证明不存在大于 7 的可达成数字。
```

 

**提示：**

- `1 <= num, t <= 50`

#### 分析

简单题，模拟即可

#### 代码

```python
class Solution:
    def theMaximumAchievableX(self, num: int, t: int) -> int:
        return num + t * 2
```



------

### 题目二、[达到末尾下标所需的最大跳跃次数](https://leetcode.cn/contest/weekly-contest-353/problems/maximum-number-of-jumps-to-reach-the-last-index/)【中等】

#### 题目描述

给你一个下标从 **0** 开始、由 `n` 个整数组成的数组 `nums` 和一个整数 `target` 。

你的初始位置在下标 `0` 。在一步操作中，你可以从下标 `i` 跳跃到任意满足下述条件的下标 `j` ：

- `0 <= i < j < n`
- `-target <= nums[j] - nums[i] <= target`

返回到达下标 `n - 1` 处所需的 **最大跳跃次数** 。

如果无法到达下标 `n - 1` ，返回 `-1` 。

 

**示例 1：**

```
输入：nums = [1,3,6,4,1,2], target = 2
输出：3
解释：要想以最大跳跃次数从下标 0 到下标 n - 1 ，可以按下述跳跃序列执行操作：
- 从下标 0 跳跃到下标 1 。 
- 从下标 1 跳跃到下标 3 。 
- 从下标 3 跳跃到下标 5 。 
可以证明，从 0 到 n - 1 的所有方案中，不存在比 3 步更长的跳跃序列。因此，答案是 3 。 
```

**示例 2：**

```
输入：nums = [1,3,6,4,1,2], target = 3
输出：5
解释：要想以最大跳跃次数从下标 0 到下标 n - 1 ，可以按下述跳跃序列执行操作：
- 从下标 0 跳跃到下标 1 。 
- 从下标 1 跳跃到下标 2 。 
- 从下标 2 跳跃到下标 3 。 
- 从下标 3 跳跃到下标 4 。 
- 从下标 4 跳跃到下标 5 。 
可以证明，从 0 到 n - 1 的所有方案中，不存在比 5 步更长的跳跃序列。因此，答案是 5 。 
```

**示例 3：**

```
输入：nums = [1,3,6,4,1,2], target = 0
输出：-1
解释：可以证明不存在从 0 到 n - 1 的跳跃序列。因此，答案是 -1 。 
```

 

**提示：**

- `2 <= nums.length == n <= 1000`
- `-10^9 <= nums[i] <= 10^9`
- `0 <= target <= 2 * 10^9`

#### 分析

动态规划

[爬楼梯](https://leetcode.cn/problems/climbing-stairs/)扩大范围版本，爬楼梯一次爬1级楼梯或者2级楼梯

这题是可以跳到多个满足`-target <= nums[j] - nums[i] <= target`的位置

`-target <= nums[j] - nums[i] <= target`  等价于 abs(nums[j] - nums[i]) <= target

#### 代码

```Python
class Solution:
    def maximumJumps(self, nums: List[int], target: int) -> int:
        n = len(nums)
        dp = [-1 for i in range(n)]
        dp[0] = 0
        for i in range(n):
            if dp[i] == -1:
                continue
            for j in range(i + 1, n):
                if abs(nums[j] - nums[i]) <= target:
                    dp[j] = max(dp[j], dp[i] + 1)
        
        return dp[n-1]
```

------

### 题目三、[构造最长非递减子数组](https://leetcode.cn/contest/weekly-contest-353/problems/longest-non-decreasing-subarray-from-two-arrays/)【中等】

#### 题目描述

给你两个下标从 **0** 开始的整数数组 `nums1` 和 `nums2` ，长度均为 `n` 。

让我们定义另一个下标从 **0** 开始、长度为 `n` 的整数数组，`nums3` 。对于范围 `[0, n - 1]` 的每个下标 `i` ，你可以将 `nums1[i]` 或 `nums2[i]` 的值赋给 `nums3[i]` 。

你的任务是使用最优策略为 `nums3` 赋值，以最大化 `nums3` 中 **最长非递减子数组** 的长度。

以整数形式表示并返回 `nums3` 中 **最长非递减** 子数组的长度。

**注意：子数组** 是数组中的一个连续非空元素序列。

 

**示例 1：**

```
输入：nums1 = [2,3,1], nums2 = [1,2,1]
输出：2
解释：构造 nums3 的方法之一是： 
nums3 = [nums1[0], nums2[1], nums2[2]] => [2,2,1]
从下标 0 开始到下标 1 结束，形成了一个长度为 2 的非递减子数组 [2,2] 。 
可以证明 2 是可达到的最大长度。
```

**示例 2：**

```
输入：nums1 = [1,3,2,1], nums2 = [2,2,3,4]
输出：4
解释：构造 nums3 的方法之一是： 
nums3 = [nums1[0], nums2[1], nums2[2], nums2[3]] => [1,2,3,4]
整个数组形成了一个长度为 4 的非递减子数组，并且是可达到的最大长度。
```

**示例 3：**

```
输入：nums1 = [1,1], nums2 = [2,2]
输出：2
解释：构造 nums3 的方法之一是： 
nums3 = [nums1[0], nums1[1]] => [1,1] 
整个数组形成了一个长度为 2 的非递减子数组，并且是可达到的最大长度。
```

 

**提示：**

- `1 <= nums1.length == nums2.length == n <= 10^5`
- `1 <= nums1[i], nums2[i] <= 10^9`

#### 分析

动态规划

子数组的长度只跟最后一个数字有关系，所以可以定义dp(i, j), i代表当前是数组中的第i个数值，j代表是选择nums1中的值还是nums2中的值。

递推的时候有两种情况：1.选择nums1中的数字，2.选择nums2中的数字

1.选择nums1中的数字：


$$
dp[i][0]=
\begin{cases}
dp[i-1][0] + 1 \quad 当nums1[i] >= nums1[i-1] \\
dp[i-1][1] + 1 \quad 当nums1[i] >= nums2[i-1]\\
1 
\end{cases}
$$
2.选择nums2中的数字
$$
dp[i][1]=
\begin{cases}
dp[i-1][0] + 1 \quad 当nums2[i] >= nums1[i-1] \\
dp[i-1][1] + 1 \quad 当nums2[i] >= nums2[i-1]\\
1 
\end{cases}
$$


#### 代码

```python
class Solution:
    def maxNonDecreasingLength(self, nums1: List[int], nums2: List[int]) -> int:
        n = len(nums1)
        dp = [[1 for i in range(2)] for j in range(n)]
        res = 1
        for i in range(1, n):
            # 选nums1
            if nums1[i] >= nums1[i-1]:
                dp[i][0] = max(dp[i-1][0] + 1, dp[i][0])
            if nums1[i] >= nums2[i-1]:
                dp[i][0] = max(dp[i-1][1] + 1, dp[i][0])
            res = max(res, dp[i][0])
            #  选nums2
            if nums2[i] >= nums1[i-1]:
                dp[i][1] = max(dp[i-1][0] + 1, dp[i][1])
            if nums2[i] >= nums2[i-1]:
                dp[i][1] = max(dp[i-1][1] + 1, dp[i][1])
            res = max(res, dp[i][1])
        return res
```

------

### 题目四、[使数组中的所有元素都等于零](https://leetcode.cn/contest/weekly-contest-353/problems/apply-operations-to-make-all-array-elements-equal-to-zero/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 和一个正整数 `k` 。

你可以对数组执行下述操作 **任意次** ：

- 从数组中选出长度为 `k` 的 **任一** 子数组，并将子数组中每个元素都 **减去** `1` 。

如果你可以使数组中的所有元素都等于 `0` ，返回 `true` ；否则，返回 `false` 。

**子数组** 是数组中的一个非空连续元素序列。

 

**示例 1：**

```
输入：nums = [2,2,3,1,1,0], k = 3
输出：true
解释：可以执行下述操作：
- 选出子数组 [2,2,3] ，执行操作后，数组变为 nums = [1,1,2,1,1,0] 。
- 选出子数组 [2,1,1] ，执行操作后，数组变为 nums = [1,1,1,0,0,0] 。
- 选出子数组 [1,1,1] ，执行操作后，数组变为 nums = [0,0,0,0,0,0] 。
```

**示例 2：**

```
输入：nums = [1,3,1,1], k = 2
输出：false
解释：无法使数组中的所有元素等于 0 。
```

 

**提示：**

- `1 <= k <= nums.length <= 10^5`
- `0 <= nums[i] <= 10^6`

#### 分析

滑动窗口

考虑第一个元素，第一个元素肯定是与后面的k-1个元素一起减1的，如果第一个元素不是这k个元素中最小的，那么这后面的k个元素肯定不满足条件，至少有个元素会被减成负数。

1.第一个元素肯定是这k个元素中最小的，处理完第一个元素之后滑动窗口往后滑动，滑动之后的第一个元素也是新的子数组中最小的。

2.每次滑动窗口都减去滑动窗口的第一个值，等价于滑动之后的新的最后一个元素加上第一个元素。

3.最后再判断一下最后窗口内的元素是否全部相等。



示例：[2,2,3,1,1,0]

![](https://github.com/hzchenxiaobin/LeetcodeContest/blob/master/resource/pic/353/353-1.png?raw=true)

![](https://github.com/hzchenxiaobin/LeetcodeContest/blob/master/resource/pic/353/353-2.png?raw=true)

最后一个窗口的元素都是3，所以返回为true

#### 代码

```python
class Solution:
    def checkArray(self, nums: List[int], k: int) -> bool:
        n = len(nums)
        l = nums[0:k]
        heapq.heapify(l)
        for i in range(n-k):
            m = heapq.heappop(l)
            pre += m
            if m != nums[i]:
                return False
            nums[i+k] += m
            heapq.heappush(l, nums[i+k])
        return max(l) == min(l)
```

