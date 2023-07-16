###### **本文主要解析LeetCode在2023年6月25日10：30组织的第【351】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-351)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/hzchenxiaobin/)**。**

---

### 题目一、[美丽下标对的数目](https://leetcode.cn/contest/weekly-contest-351/problems/number-of-beautiful-pairs/)【简单】

#### 题目描述

给你一个下标从 **0** 开始的整数数组 `nums` 。如果下标对 `i`、`j` 满足 `0 ≤ i < j < nums.length` ，如果 `nums[i]` 的 **第一个数字** 和 `nums[j]` 的 **最后一个数字** **互质** ，则认为 `nums[i]` 和 `nums[j]` 是一组 **美丽下标对** 。

返回 `nums` 中 **美丽下标对** 的总数目。

对于两个整数 `x` 和 `y` ，如果不存在大于 1 的整数可以整除它们，则认为 `x` 和 `y` **互质** 。换而言之，如果 `gcd(x, y) == 1` ，则认为 `x` 和 `y` 互质，其中 `gcd(x, y)` 是 `x` 和 `k` **最大公因数** 。

 

**示例 1：**

```
输入：nums = [2,5,1,4]
输出：5
解释：nums 中共有 5 组美丽下标对：
i = 0 和 j = 1 ：nums[0] 的第一个数字是 2 ，nums[1] 的最后一个数字是 5 。2 和 5 互质，因此 gcd(2,5) == 1 。
i = 0 和 j = 2 ：nums[0] 的第一个数字是 2 ，nums[1] 的最后一个数字是 1 。2 和 5 互质，因此 gcd(2,1) == 1 。
i = 1 和 j = 2 ：nums[0] 的第一个数字是 5 ，nums[1] 的最后一个数字是 1 。2 和 5 互质，因此 gcd(5,1) == 1 。
i = 1 和 j = 3 ：nums[0] 的第一个数字是 5 ，nums[1] 的最后一个数字是 4 。2 和 5 互质，因此 gcd(5,4) == 1 。
i = 2 和 j = 3 ：nums[0] 的第一个数字是 1 ，nums[1] 的最后一个数字是 4 。2 和 5 互质，因此 gcd(1,4) == 1 。
因此，返回 5 。
```

**示例 2：**

```
输入：nums = [11,21,12]
输出：2
解释：共有 2 组美丽下标对：
i = 0 和 j = 1 ：nums[0] 的第一个数字是 1 ，nums[1] 的最后一个数字是 1 。gcd(1,1) == 1 。
i = 0 和 j = 2 ：nums[0] 的第一个数字是 1 ，nums[1] 的最后一个数字是 2 。gcd(1,2) == 1 。
因此，返回 2 。
```

 

**提示：**

- `2 <= nums.length <= 100`
- `1 <= nums[i] <= 9999`
- `nums[i] % 10 != 0`

#### 分析

简单题，按题意模拟即可

#### 代码

```python
class Solution:
    def countBeautifulPairs(self, nums: List[int]) -> int:
        n = len(nums)
        res = 0
        for i in range(n):
            for j in range(i + 1, n):
                x, y = int(str(nums[i])[0]), int(str(nums[j])[-1])
                res += gcd(x, y) == 1
        return res
```



------

### 题目二、[得到整数零需要执行的最少操作数](https://leetcode.cn/contest/weekly-contest-351/problems/minimum-operations-to-make-the-integer-zero/)【中等】

#### 题目描述

给你两个整数：`num1` 和 `num2` 。

在一步操作中，你需要从范围 `[0, 60]` 中选出一个整数 `i` ，并从 `num1` 减去 `2i + num2` 。

请你计算，要想使 `num1` 等于 `0` 需要执行的最少操作数，并以整数形式返回。

如果无法使 `num1` 等于 `0` ，返回 `-1` 。

 

**示例 1：**

```
输入：num1 = 3, num2 = -2
输出：3
解释：可以执行下述步骤使 3 等于 0 ：
- 选择 i = 2 ，并从 3 减去 22 + (-2) ，num1 = 3 - (4 + (-2)) = 1 。
- 选择 i = 2 ，并从 1 减去 22 + (-2) ，num1 = 1 - (4 + (-2)) = -1 。
- 选择 i = 0 ，并从 -1 减去 20 + (-2) ，num1 = (-1) - (1 + (-2)) = 0 。
可以证明 3 是需要执行的最少操作数。
```

**示例 2：**

```
输入：num1 = 5, num2 = 7
输出：-1
解释：可以证明，执行操作无法使 5 等于 0 。
```

 

**提示：**

- `1 <= num1 <= 10^9`
- `-10^9 <= num2 <= 10^9`

#### 分析

第i次时的等式为
$$
num1 = \sum_{k=0}^i2^x + i * num2
$$
转换一下：
$$
num1 - i * num2 = \sum_{k=0}^i2^x
$$
令 k = num1 - i * num2

k可以表示成i个2的幂的和的条件是 

1.k >= i 因为2的幂最小值是1， 所以i个2的幂的和大于等于1

2.i >= k的二进制表示中1的个数， 比如19 -> 10011(二进制表示) -> 2^0 + 2 ^1 + 2^4 这是最少次数的2的幂的和



所以满足题意的表达式为：

num1- i * num2 的二进制表示中1的个数 < = i  < num1 - i * num2 



#### 代码

```Python
class Solution:
    def makeTheIntegerZero(self, num1: int, num2: int) -> int:
        i = 0
        print(bin(19))
        while num1 - i * num2 >= i:
            if i >= (num1 - i * num2).bit_count():
                return i
            i += 1
        return -1
```

------

### 题目三、[将数组划分成若干好子数组的方式](https://leetcode.cn/contest/weekly-contest-351/problems/ways-to-split-array-into-good-subarrays/)【中等】

#### 题目描述

给你一个二元数组 `nums` 。

如果数组中的某个子数组 **恰好** 只存在 **一** 个值为 `1` 的元素，则认为该子数组是一个 **好子数组** 。

请你统计将数组 `nums` 划分成若干 **好子数组** 的方法数，并以整数形式返回。由于数字可能很大，返回其对 `109 + 7` **取余** 之后的结果。

子数组是数组中的一个连续 **非空** 元素序列。

 

**示例 1：**

```
输入：nums = [0,1,0,0,1]
输出：3
解释：存在 3 种可以将 nums 划分成若干好子数组的方式：
- [0,1] [0,0,1]
- [0,1,0] [0,1]
- [0,1,0,0] [1]
```

**示例 2：**

```
输入：nums = [0,1,0]
输出：1
解释：存在 1 种可以将 nums 划分成若干好子数组的方式：
- [0,1,0]
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `0 <= nums[i] <= 1`

#### 分析

满足题意的结果是：**1的间隔数字相乘的结果**

比如0100101

可以将该数组拆分成3个子数组，我们可以看成插入两个逗号，那么逗号插入在什么位置呢？

1.第一个逗号是插入在01之后的位置，下一个1的位置之前：

01,00101或者010,0101或者0100,101

2.第二个逗号插入在101之间：

01001,01或者010010,1

最终的结果是这两个逗号的排列组合也就是3 * 2 = 6

#### 代码

```python
class Solution:
    def numberOfGoodSubarraySplits(self, nums: List[int]) -> int:
        MOD = 10 ** 9 + 7
        arr = list()
        for i, num in enumerate(nums):
            if num == 1:
                arr.append(i)
        res = 1
        for i in range(1, len(arr)):
            res *= arr[i] - arr[i-1]
            res %= MOD
        return res if len(arr) else 0
```

------

### 题目四、[机器人碰撞](https://leetcode.cn/contest/weekly-contest-351/problems/robot-collisions/)【困难】

#### 题目描述

现有 `n` 个机器人，编号从 **1** 开始，每个机器人包含在路线上的位置、健康度和移动方向。

给你下标从 **0** 开始的两个整数数组 `positions`、`healths` 和一个字符串 `directions`（`directions[i]` 为 **'L'** 表示 **向左** 或 **'R'** 表示 **向右**）。 `positions` 中的所有整数 **互不相同** 。

所有机器人以 **相同速度** **同时** 沿给定方向在路线上移动。如果两个机器人移动到相同位置，则会发生 **碰撞** 。

如果两个机器人发生碰撞，则将 **健康度较低** 的机器人从路线中 **移除** ，并且另一个机器人的健康度 **减少 1** 。幸存下来的机器人将会继续沿着与之前 **相同** 的方向前进。如果两个机器人的健康度相同，则将二者都从路线中移除。

请你确定全部碰撞后幸存下的所有机器人的 **健康度** ，并按照原来机器人编号的顺序排列。即机器人 1 （如果幸存）的最终健康度，机器人 2 （如果幸存）的最终健康度等。 如果不存在幸存的机器人，则返回空数组。

在不再发生任何碰撞后，请你以数组形式，返回所有剩余机器人的健康度（按机器人输入中的编号顺序）。

**注意：**位置 `positions` 可能是乱序的。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2023/05/15/image-20230516011718-12.png)

```
输入：positions = [5,4,3,2,1], healths = [2,17,9,15,10], directions = "RRRRR"
输出：[2,17,9,15,10]
解释：在本例中不存在碰撞，因为所有机器人向同一方向移动。所以，从第一个机器人开始依序返回健康度，[2, 17, 9, 15, 10] 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2023/05/15/image-20230516004433-7.png)

```
输入：positions = [3,5,2,6], healths = [10,10,15,12], directions = "RLRL"
输出：[14]
解释：本例中发生 2 次碰撞。首先，机器人 1 和机器人 2 将会碰撞，因为二者健康度相同，二者都将被从路线中移除。接下来，机器人 3 和机器人 4 将会发生碰撞，由于机器人 4 的健康度更小，则它会被移除，而机器人 3 的健康度变为 15 - 1 = 14 。仅剩机器人 3 ，所以返回 [14] 。
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2023/05/15/image-20230516005114-9.png)

```
输入：positions = [1,2,5,6], healths = [10,10,11,11], directions = "RLRL"
输出：[]
解释：机器人 1 和机器人 2 将会碰撞，因为二者健康度相同，二者都将被从路线中移除。机器人 3 和机器人 4 将会碰撞，因为二者健康度相同，二者都将被从路线中移除。所以返回空数组 [] 。
```

 

**提示：**

- `1 <= positions.length == healths.length == directions.length == n <= 10^5`
- `1 <= positions[i], healths[i] <= 10^9`
- `directions[i] == 'L'` 或 `directions[i] == 'R'`
- `positions` 中的所有值互不相同

#### 分析

栈的模拟题

不需要考虑机器人最终所在的位置，只需要考虑碰撞的情况。

1.按照坐标位置进行排序

2.如果是向右的则加入栈中

3.如果是向左，则按照题意处理碰撞情况

4.最终构造返回结果即可

#### 代码

```python
class Solution:
    def survivedRobotsHealths(self, positions: List[int], healths: List[int], directions: str) -> List[int]:
        arr = sorted(zip(positions, healths, directions, range(len(positions))))
        
        stack = list()
        for t in arr:
            health, direction, index= t[1], t[2], t[3]
            # 如果是向右的则直接加入栈中
            if direction == 'R':
                stack.append([health, direction, index])
                continue
            
            # 如果栈顶不为空且方向是向右的则肯定会碰撞
            while len(stack) > 0  and stack[-1][1] == 'R':
                pop = stack.pop()
                health_pop = pop[0]
                # 如果两个的健康值相等，则两个都消失
                if health == health_pop:
                    health = 0
                    break
                # 如果左方向的health 小于 右方向的health，则右方向的health减1，并且仍然放置在栈顶
                if health < health_pop:
                    health = 0
                    pop[0] -= 1
                    stack.append(pop)
                    break
                # 如果右方向的health 小于 左方向的health，则左方向的health减1，继续与栈顶比较
                if health > health_pop:
                    health -= 1
            if health > 0:
                stack.append([health, direction, index])
        
        # 按照输入顺序构造返回值
        stack.sort(key=lambda x:x[2])
        return [s[0] for s in stack]
```

