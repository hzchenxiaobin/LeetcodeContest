###### **本文主要解析LeetCode在2023年6月18日10：30组织的第【350】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-350)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/chen-xiao-bin-5/)**。**

---

### 题目一、[总行驶距离](https://leetcode.cn/contest/weekly-contest-350/problems/total-distance-traveled/)【简单】

#### 题目描述

卡车有两个油箱。给你两个整数，`mainTank` 表示主油箱中的燃料（以升为单位），`additionalTank` 表示副油箱中的燃料（以升为单位）。

该卡车每耗费 `1` 升燃料都可以行驶 `10` km。每当主油箱使用了 `5` 升燃料时，如果副油箱至少有 `1` 升燃料，则会将 `1` 升燃料从副油箱转移到主油箱。

返回卡车可以行驶的最大距离。

注意：从副油箱向主油箱注入燃料不是连续行为。这一事件会在每消耗 `5` 升燃料时突然且立即发生。

 

**示例 1：**

```
输入：mainTank = 5, additionalTank = 10
输出：60
解释：
在用掉 5 升燃料后，主油箱中燃料还剩下 (5 - 5 + 1) = 1 升，行驶距离为 50km 。
在用掉剩下的 1 升燃料后，没有新的燃料注入到主油箱中，主油箱变为空。
总行驶距离为 60km 。
```

**示例 2：**

```
输入：mainTank = 1, additionalTank = 2
输出：10
解释：
在用掉 1 升燃料后，主油箱变为空。
总行驶距离为 10km 。
```

 

**提示：**

- `1 <= mainTank, additionalTank <= 100`

#### 分析

模拟题，按照题意进行模拟即可

#### 代码

```python
class Solution:
    def distanceTraveled(self, mainTank: int, additionalTank: int) -> int:
        res = 0
        while mainTank >= 5:
            res += 50
            mainTank -= 5
            if additionalTank >= 1:
                mainTank += 1
                additionalTank -= 1
        res += mainTank * 10
        return res
```



------

### 题目二、[找出分区值](https://leetcode.cn/contest/weekly-contest-350/problems/find-the-value-of-the-partition/)【中等】

#### 题目描述

给你一个 **正** 整数数组 `nums` 。

将 `nums` 分成两个数组：`nums1` 和 `nums2` ，并满足下述条件：

- 数组 `nums` 中的每个元素都属于数组 `nums1` 或数组 `nums2` 。
- 两个数组都 **非空** 。
- 分区值 **最小** 。

分区值的计算方法是 `|max(nums1) - min(nums2)|` 。

其中，`max(nums1)` 表示数组 `nums1` 中的最大元素，`min(nums2)` 表示数组 `nums2` 中的最小元素。

返回表示分区值的整数。

 

**示例 1：**

```
输入：nums = [1,3,2,4]
输出：1
解释：可以将数组 nums 分成 nums1 = [1,2] 和 nums2 = [3,4] 。
- 数组 nums1 的最大值等于 2 。
- 数组 nums2 的最小值等于 3 。
分区值等于 |2 - 3| = 1 。
可以证明 1 是所有分区方案的最小值。
```

**示例 2：**

```
输入：nums = [100,1,10]
输出：9
解释：可以将数组 nums 分成 nums1 = [10] 和 nums2 = [100,1] 。 
- 数组 nums1 的最大值等于 10 。 
- 数组 nums2 的最小值等于 1 。 
分区值等于 |10 - 1| = 9 。 
可以证明 9 是所有分区方案的最小值。
```

 

**提示：**

- `2 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^9`

#### 分析

分区值的大小为|max(nums1) - min(nums2)|

将数组排序，然后分割成两个连续的子数组，相邻两个元素相减的值即为这个切分方法的分区值，取得分区值最小值，也就转化成相邻元素相减的最小值。

#### 代码

```Python
class Solution:
    def findValueOfPartition(self, nums: List[int]) -> int:
        nums.sort()
        res = inf
        for i in range(1, len(nums)):
            res = min(nums[i] - nums[i-1], res)
        return res
```

------

### 题目三、[特别的排列](https://leetcode.cn/contest/weekly-contest-350/problems/special-permutations/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` ，它包含 `n` 个 **互不相同** 的正整数。如果 `nums` 的一个排列满足以下条件，我们称它是一个特别的排列：

- 对于 `0 <= i < n - 1` 的下标 `i` ，要么 `nums[i] % nums[i+1] == 0` ，要么 `nums[i+1] % nums[i] == 0` 。

请你返回特别排列的总数目，由于答案可能很大，请将它对 `109 + 7` **取余** 后返回。

 

**示例 1：**

```
输入：nums = [2,3,6]
输出：2
解释：[3,6,2] 和 [2,6,3] 是 nums 两个特别的排列。
```

**示例 2：**

```
输入：nums = [1,4,3]
输出：2
解释：[3,1,4] 和 [4,1,3] 是 nums 两个特别的排列。
```

 

**提示：**

- `2 <= nums.length <= 14`
- `1 <= nums[i] <= 10^9`

#### 分析

如果列出数字排列的所有组合，则时间复杂度为14! * 10，则会TLE

***性质：如果前面的数字相同（排列不同）并且最后一个数字也相同的情况下，后面的排列个数是一样的。***

比如：[1, 2, 4, 8, 16]，排列的前三个数都是1,2,4并且最后一个数是4的情况下，后面的排列个数都是2。

![image-20230624213430138](/Users/chenbinbin/Library/Application Support/typora-user-images/image-20230624213430138.png)

所以在这里可以做记忆化递归，记录最后一个数字和数字的使用情况，可以记忆最后一个数字和数字的使用情况的的时候的返回值，不需要重复计算。

此时的时间复杂度为：最后一个数字有n种，数字的的使用情况是2^n，单次递归的时间复杂度为n，所以总的时间复杂度为 n^2 * 2^n



数字的使用情况可以用二进制来表示，以n=5为例：

当所有的数字都没被使用时，二进制的值为：11111

当第一个数字被使用时，二进制的值为：11110

以此类推。

当所有的值被使用完了，也就是二进制的值为0时，递归结束。

#### 代码

```python
class Solution:
    def specialPerm(self, nums: List[int]) -> int:
        n = len(nums)
        
        @cache
        def dfs(i:int, j:int):
            if i == 0:
                return 1
            res = 0
            for idx, num in enumerate(nums):
                if (i >> idx) & 1 and (num % nums[j] == 0 or nums[j] % num == 0):
                    res += dfs((1 << idx) ^ i, idx)
            return res
        u = 2 ** n - 1
        return sum(dfs(u ^ (1 << i), i) for i in range(n)) % (10 ** 9 + 7)
```

------

### 题目四、[给墙壁刷油漆](https://leetcode.cn/contest/weekly-contest-350/problems/painting-the-walls/)【困难】

#### 题目描述

给你两个长度为 `n` 下标从 **0** 开始的整数数组 `cost` 和 `time` ，分别表示给 `n` 堵不同的墙刷油漆需要的开销和时间。你有两名油漆匠：

- 一位需要 **付费** 的油漆匠，刷第 `i` 堵墙需要花费 `time[i]` 单位的时间，开销为 `cost[i]` 单位的钱。
- 一位 **免费** 的油漆匠，刷 **任意** 一堵墙的时间为 `1` 单位，开销为 `0` 。但是必须在付费油漆匠 **工作** 时，免费油漆匠才会工作。

请你返回刷完 `n` 堵墙最少开销为多少。



**示例 1：**

```
输入：cost = [1,2,3,2], time = [1,2,3,2]
输出：3
解释：下标为 0 和 1 的墙由付费油漆匠来刷，需要 3 单位时间。同时，免费油漆匠刷下标为 2 和 3 的墙，需要 2 单位时间，开销为 0 。总开销为 1 + 2 = 3 。
```

**示例 2：**

```
输入：cost = [2,3,4,2], time = [1,1,1,1]
输出：4
解释：下标为 0 和 3 的墙由付费油漆匠来刷，需要 2 单位时间。同时，免费油漆匠刷下标为 1 和 2 的墙，需要 2 单位时间，开销为 0 。总开销为 2 + 2 = 4 。
```

 

**提示：**

- `1 <= cost.length <= 500`
- `cost.length == time.length`
- `1 <= cost[i] <= 10^6`
- `1 <= time[i] <= 500`

#### 分析



#### 代码

```python
class Solution:
    def paintWalls(self, cost: List[int], time: List[int]) -> int:
        
        @cache
        def dfs(i:int, j:int) -> int:
            if j >= i: return 0
            if i < 0: return inf
            return min(dfs(i-1, j + time[i]) + cost[i], dfs(i-1, j-1))
        
        return dfs(len(cost) - 1, 0)
```

