###### **本文主要解析LeetCode在2023年7月2日10：30组织的第【352】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-352)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/chen-xiao-bin-5/)**。**

---

### 题目一、[最长奇偶子数组](https://leetcode.cn/contest/weekly-contest-352/problems/longest-even-odd-subarray-with-threshold/)【简单】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 和一个整数 `threshold` 。

请你从 `nums` 的子数组中找出以下标 `l` 开头、下标 `r` 结尾 `(0 <= l <= r < nums.length)` 且满足以下条件的 **最长子数组** ：

- `nums[l] % 2 == 0`
- 对于范围 `[l, r - 1]` 内的所有下标 `i` ，`nums[i] % 2 != nums[i + 1] % 2`
- 对于范围 `[l, r]` 内的所有下标 `i` ，`nums[i] <= threshold`

以整数形式返回满足题目要求的最长子数组的长度。

**注意：子数组** 是数组中的一个连续非空元素序列。

 

**示例 1：**

```
输入：nums = [3,2,5,4], threshold = 5
输出：3
解释：在这个示例中，我们选择从 l = 1 开始、到 r = 3 结束的子数组 => [2,5,4] ，满足上述条件。
因此，答案就是这个子数组的长度 3 。可以证明 3 是满足题目要求的最大长度。
```

**示例 2：**

```
输入：nums = [1,2], threshold = 2
输出：1
解释：
在这个示例中，我们选择从 l = 1 开始、到 r = 1 结束的子数组 => [2] 。
该子数组满足上述全部条件。可以证明 1 是满足题目要求的最大长度。
```

**示例 3：**

```
输入：nums = [2,3,4,5], threshold = 4
输出：3
解释：
在这个示例中，我们选择从 l = 0 开始、到 r = 2 结束的子数组 => [2,3,4] 。 
该子数组满足上述全部条件。
因此，答案就是这个子数组的长度 3 。可以证明 3 是满足题目要求的最大长度。
```

 

**提示：**

- `1 <= nums.length <= 100`
- `1 <= nums[i] <= 100`
- `1 <= threshold <= 100`

#### 分析

模拟题，按照题意模拟：

1.枚举左边界l，如果满足nums[l] % 2 == 0，则进入2。

2.枚举右边界r，如果满足2和3，则更新子数组长度的最大值，否则结束循环。

#### 代码

```python
class Solution:
    def longestAlternatingSubarray(self, nums: List[int], threshold: int) -> int:
        n = len(nums)
        res = 0
        for l in range(n):
            if nums[l] % 2 != 0:
                continue
            for r in range(l, n):
                if nums[r] > threshold:
                    break
                if r > l and nums[r-1] % 2 == nums[r] % 2:
                    break
                res = max(res, r - l + 1)
                
        return res
```



------

### 题目二、[和等于目标值的质数对](https://leetcode.cn/contest/weekly-contest-352/problems/prime-pairs-with-target-sum/)【中等】

#### 题目描述

给你一个整数 `n` 。如果两个整数 `x` 和 `y` 满足下述条件，则认为二者形成一个质数对：

- `1 <= x <= y <= n`
- `x + y == n`
- `x` 和 `y` 都是质数

请你以二维有序列表的形式返回符合题目要求的所有 `[xi, yi]` ，列表需要按 `xi` 的 **非递减顺序** 排序。如果不存在符合要求的质数对，则返回一个空数组。

**注意：**质数是大于 `1` 的自然数，并且只有两个因子，即它本身和 `1` 。

 

**示例 1：**

```
输入：n = 10
输出：[[3,7],[5,5]]
解释：在这个例子中，存在满足条件的两个质数对。 
这两个质数对分别是 [3,7] 和 [5,5]，按照题面描述中的方式排序后返回。
```

**示例 2：**

```
输入：n = 2
输出：[]
解释：可以证明不存在和为 2 的质数对，所以返回一个空数组。 
```

 

**提示：**

- `1 <= n <= 10^6`

#### 分析

预先算出小于10^6的所有质数，然后遍历即可。

使用[埃氏筛](https://oi-wiki.org/math/number-theory/sieve/)可以比较快的求出所有质数。

埃氏筛的主要思路：对于任意一个大于1的正整数n，那么它的n倍就是合数(x > 1)。利用这个结论，我们可以避免很多次不必要的检测。

#### 代码

```Python
# 埃氏筛求质数
prime = set()
mx = 10 ** 6 + 1
is_prime = [True] * mx
for i in range(2, mx):
    if is_prime[i]:
        prime.add(i)
        for j in range(i * i, mx, i):
            is_prime[j] = False

class Solution:
    def findPrimePairs(self, n: int) -> List[List[int]]:
        res = list()
        visited = set()
        for i in range(n):
            if i not in visited and i in prime and n - i in prime:
                res.append([i, n - i])
                visited.add(i)
                visited.add(n-i)
        return res 
```

------

### 题目三、[不间断子数组](https://leetcode.cn/contest/weekly-contest-352/problems/continuous-subarrays/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 。`nums` 的一个子数组如果满足以下条件，那么它是 **不间断** 的：

- `i`，`i + 1` ，...，`j` 表示子数组中的下标。对于所有满足 `i <= i1, i2 <= j` 的下标对，都有 `0 <= |nums[i1] - nums[i2]| <= 2` 。

请你返回 **不间断** 子数组的总数目。

子数组是一个数组中一段连续 **非空** 的元素序列。

 

**示例 1：**

```
输入：nums = [5,4,2,4]
输出：8
解释：
大小为 1 的不间断子数组：[5], [4], [2], [4] 。
大小为 2 的不间断子数组：[5,4], [4,2], [2,4] 。
大小为 3 的不间断子数组：[4,2,4] 。
没有大小为 4 的不间断子数组。
不间断子数组的总数目为 4 + 3 + 1 = 8 。
除了这些以外，没有别的不间断子数组。
```

**示例 2：**

```
输入：nums = [1,2,3]
输出：6
解释：
大小为 1 的不间断子数组：[1], [2], [3] 。
大小为 2 的不间断子数组：[1,2], [2,3] 。
大小为 3 的不间断子数组：[1,2,3] 。
不间断子数组的总数目为 3 + 2 + 1 = 6 。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^9`

#### 分析

滑动窗口

维护一个滑动窗口，使得滑动窗口内的所有元素满足差的绝对值小于等于2。

1.左边界：滑动窗口的起始索引

2.右边界：以右边界索引对应的元素作为子数组的结束元素，所以右边界每当向前进一位时，左边界移动到符合条件的位置后，子数组的个数就是滑动窗口的个数，也就是r - l + 1。



**示例：**[5, 4, 2]

第一步：

起始时：l = 0, r = 0, 窗口内的元素为[5]

规则判断：符合规则，所以最终有效窗口内的元素就是[5]

结果：只有一个子数组，所以结果加1



第二步：

起始时：l = 0, r = 1, 窗口内的元素为[4, 5]

规则判断：符合规则，所以最终有效窗口内的元素就是[4, 5]

结果：窗口内有两个以5结尾的子数组：[4, 5], [5]，所以结果加2



第三步：

起始时：l = 0, r = 2, 窗口内的元素为[2, 4, 5]

规则判断：不符合规则，l往前移动一步，将nums[l]在窗口中去掉，也就是去掉5。去掉5之后满足规则，所以最终有效窗口内的元素就是[2， 4]

结果：窗口内有两个以2结尾的子数组：[4， 2], [2]，所以结果加2



#### 代码

```python
from sortedcontainers import SortedList
class Solution:
    def continuousSubarrays(self, nums: List[int]) -> int:
        sortList = SortedList()
        res = 0
        l = 0
        
        for (r, num) in enumerate(nums):
            sortList.add(num)
            while sortList[-1] - sortList[0] > 2:
                sortList.remove(nums[l])
                l += 1
            res += r - l + 1
        
        return res
```

------

### 题目四、[所有子数组中不平衡数字之和](https://leetcode.cn/contest/weekly-contest-352/problems/sum-of-imbalance-numbers-of-all-subarrays/)【困难】

#### 题目描述

一个长度为 `n` 下标从 **0** 开始的整数数组 `arr` 的 **不平衡数字** 定义为，在 `sarr = sorted(arr)` 数组中，满足以下条件的下标数目：

- `0 <= i < n - 1` ，和
- `sarr[i+1] - sarr[i] > 1`

这里，`sorted(arr)` 表示将数组 `arr` 排序后得到的数组。

给你一个下标从 **0** 开始的整数数组 `nums` ，请你返回它所有 **子数组** 的 **不平衡数字** 之和。

子数组指的是一个数组中连续一段 **非空** 的元素序列。

 

**示例 1：**

```
输入：nums = [2,3,1,4]
输出：3
解释：总共有 3 个子数组有非 0 不平衡数字：
- 子数组 [3, 1] ，不平衡数字为 1 。
- 子数组 [3, 1, 4] ，不平衡数字为 1 。
- 子数组 [1, 4] ，不平衡数字为 1 。
其他所有子数组的不平衡数字都是 0 ，所以所有子数组的不平衡数字之和为 3 。
```

**示例 2：**

```
输入：nums = [1,3,3,3,5]
输出：8
解释：总共有 7 个子数组有非 0 不平衡数字：
- 子数组 [1, 3] ，不平衡数字为 1 。
- 子数组 [1, 3, 3] ，不平衡数字为 1 。
- 子数组 [1, 3, 3, 3] ，不平衡数字为 1 。
- 子数组 [1, 3, 3, 3, 5] ，不平衡数字为 2 。
- 子数组 [3, 3, 3, 5] ，不平衡数字为 1 。
- 子数组 [3, 3, 5] ，不平衡数字为 1 。
- 子数组 [3, 5] ，不平衡数字为 1 。
其他所有子数组的不平衡数字都是 0 ，所以所有子数组的不平衡数字之和为 8 。
```

 

**提示：**

- `1 <= nums.length <= 1000`
- `1 <= nums[i] <= nums.length`

#### 分析

由于数据量比较小，两次for循环直接模拟即可。

在for循环中，模拟数据插入的动作，如果插入时该元素减左边的元素大于1，则不平衡数字加1.



**示例：**[1, 5, 3]

第一次循环：

第一步：

插入1，结果为[1]， 总平衡数字为0



第二步：

插入5，结果为[1, 5], 5 - 1 > 2，所以 总平衡数字加1，最终为1



第三步：

插入3， 结果为[1, 3, 5], 3 - 1 > 2并且5 - 3 > 1，所以不平衡数字加2

但是由于这个数字的插入，导致原有的[1, 5]不平衡数字没了，所以要减1.

最终的平衡数字就是1 + 2 - 1 = 2。



第二次循环：

以此类推



#### 代码

```python
from sortedcontainers import SortedList

class Solution:
    def sumImbalanceNumbers(self, nums: List[int]) -> int:
        n = len(nums)
        res = 0
        
        for l in range(n):
            sl = SortedList([nums[l]])
            count = 0
            for r in range(l + 1, n):
                num = nums[r]
                # 新的元素要插入的位置
                index = sl.bisect_left(num)
                # 如果比左边的值大于1， 则不平衡数字加1
                if index > 0 and num - sl[index - 1] > 1:
                    count += 1
                # 如果比左边的值小于1， 则不平衡数字加1
                if index < len(sl) and sl[index] - num > 1:
                    count += 1
                # 由于插入导致原来的不平衡数字减少1，则减1
                if index > 0 and index < len(sl) and sl[index] - sl[index - 1] > 1:
                    count -= 1
                sl.add(num)
                res += count
        
        return res
```

