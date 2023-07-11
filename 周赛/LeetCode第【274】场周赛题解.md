### 题目一、[2124. 检查是否所有 A 都在 B 之前](https://leetcode-cn.com/problems/check-if-all-as-appears-before-all-bs/)【简单】

给你一个 **仅** 由字符 `'a'` 和 `'b'` 组成的字符串 `s` 。如果字符串中 **每个** `'a'` 都出现在 **每个** `'b'` 之前，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

```
输入：s = "aaabbb"
输出：true
解释：
'a' 位于下标 0、1 和 2 ；而 'b' 位于下标 3、4 和 5 。
因此，每个 'a' 都出现在每个 'b' 之前，所以返回 true 。
```

**示例 2：**

```
输入：s = "abab"
输出：false
解释：
存在一个 'a' 位于下标 2 ，而一个 'b' 位于下标 1 。
因此，不能满足每个 'a' 都出现在每个 'b' 之前，所以返回 false 。
```

**示例 3：**

```
输入：s = "bbb"
输出：true
解释：
不存在 'a' ，因此可以视作每个 'a' 都出现在每个 'b' 之前，所以返回 true 。
```

 

**提示：**

- `1 <= s.length <= 100`
- `s[i]` 为 `'a'` 或 `'b'`



#### 分析

如果字符串中存在"ba"则说明不符合题意，返回false，如果不存在"ba"则复合题意。



#### 代码

```python
class Solution:
    def checkString(self, s: str) -> bool:
        return 'ba' not in s
```



------

### 题目二、[2125. 银行中的激光束数量](https://leetcode-cn.com/problems/number-of-laser-beams-in-a-bank/)【中等】

银行内部的防盗安全装置已经激活。给你一个下标从 **0** 开始的二进制字符串数组 `bank` ，表示银行的平面图，这是一个大小为 `m x n` 的二维矩阵。 `bank[i]` 表示第 `i` 行的设备分布，由若干 `'0'` 和若干 `'1'` 组成。`'0'` 表示单元格是空的，而 `'1'` 表示单元格有一个安全设备。

对任意两个安全设备而言，**如果****同时** 满足下面两个条件，则二者之间存在 **一个** 激光束：

- 两个设备位于两个 **不同行** ：`r1` 和 `r2` ，其中 `r1 < r2` 。
- 满足 `r1 < i < r2` 的 **所有** 行 `i` ，都 **没有安全设备** 。

激光束是独立的，也就是说，一个激光束既不会干扰另一个激光束，也不会与另一个激光束合并成一束。

返回银行中激光束的总数量。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/12/24/laser1.jpg)

```
输入：bank = ["011001","000000","010100","001000"]
输出：8
解释：在下面每组设备对之间，存在一条激光束。总共是 8 条激光束：
 * bank[0][1] -- bank[2][1]
 * bank[0][1] -- bank[2][3]
 * bank[0][2] -- bank[2][1]
 * bank[0][2] -- bank[2][3]
 * bank[0][5] -- bank[2][1]
 * bank[0][5] -- bank[2][3]
 * bank[2][1] -- bank[3][2]
 * bank[2][3] -- bank[3][2]
注意，第 0 行和第 3 行上的设备之间不存在激光束。
这是因为第 2 行存在安全设备，这不满足第 2 个条件。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/12/24/laser2.jpg)

```
输入：bank = ["000","111","000"]
输出：0
解释：不存在两个位于不同行的设备
```

 

**提示：**

- `m == bank.length`
- `n == bank[i].length`
- `1 <= m, n <= 500`
- `bank[i][j]` 为 `'0'` 或 `'1'`



#### 分析

计算每一行1的个数，与上一行1的个数相乘，然后全部相加即可



#### 代码

```python
class Solution:
    def numberOfBeams(self, bank: List[str]) -> int:
        result = 0
        pre = 0
        for str in bank:
            count = str.count('1')
            if not count:
                continue
            result += count * pre
            pre = count
        return result
```



------

### 题目三、[2126. 摧毁小行星](https://leetcode-cn.com/problems/destroying-asteroids/)【中等】

给你一个整数 `mass` ，它表示一颗行星的初始质量。再给你一个整数数组 `asteroids` ，其中 `asteroids[i]` 是第 `i` 颗小行星的质量。

你可以按 **任意顺序** 重新安排小行星的顺序，然后让行星跟它们发生碰撞。如果行星碰撞时的质量 **大于等于** 小行星的质量，那么小行星被 **摧毁** ，并且行星会 **获得** 这颗小行星的质量。否则，行星将被摧毁。

如果所有小行星 **都** 能被摧毁，请返回 `true` ，否则返回 `false` 。

 

**示例 1：**

```
输入：mass = 10, asteroids = [3,9,19,5,21]
输出：true
解释：一种安排小行星的方式为 [9,19,5,3,21] ：
- 行星与质量为 9 的小行星碰撞。新的行星质量为：10 + 9 = 19
- 行星与质量为 19 的小行星碰撞。新的行星质量为：19 + 19 = 38
- 行星与质量为 5 的小行星碰撞。新的行星质量为：38 + 5 = 43
- 行星与质量为 3 的小行星碰撞。新的行星质量为：43 + 3 = 46
- 行星与质量为 21 的小行星碰撞。新的行星质量为：46 + 21 = 67
所有小行星都被摧毁。
```

**示例 2：**

```
输入：mass = 5, asteroids = [4,9,23,4]
输出：false
解释：
行星无论如何没法获得足够质量去摧毁质量为 23 的小行星。
行星把别的小行星摧毁后，质量为 5 + 4 + 9 + 4 = 22 。
它比 23 小，所以无法摧毁最后一颗小行星。
```

 

**提示：**

- `1 <= mass <= 10^5`
- `1 <= asteroids.length <= 10^5`
- `1 <= asteroids[i] <= 10^5`



#### 分析

从小到大摧毁行星即可



#### 代码

```python
class Solution:
    def asteroidsDestroyed(self, mass: int, asteroids: List[int]) -> bool:
        asteroids.sort()
        for asteroid in asteroids:
            if mass >= asteroid:
                mass += asteroid
            else:
                return False
        return True
```

------

### 题目四、[2127. 参加会议的最多员工数](https://leetcode-cn.com/problems/maximum-employees-to-be-invited-to-a-meeting/)【困难】