###### 本文主要解析LeetCode在2021年12月12日10：30组织的第【271】场周赛题目，[竞赛链接](https://leetcode-cn.com/contest/weekly-contest-271)。

###### 有兴趣的同学可以关注一下我的LeetCode[个人账号](https://leetcode-cn.com/u/chen-xiao-bin-5/)。

###### 周赛群人数过多，只能通过邀请进群，有兴趣一起打周赛的同学可以添加我的微信号：cbbdwx，拉你进群

------

### 题目一、[5952. 环和杆](https://leetcode-cn.com/problems/rings-and-rods/)【简单】

#### 题目描述

总计有 `n` 个环，环的颜色可以是红、绿、蓝中的一种。这些环分布穿在 10 根编号为 `0` 到 `9` 的杆上。

给你一个长度为 `2n` 的字符串 `rings` ，表示这 `n` 个环在杆上的分布。`rings` 中每两个字符形成一个 **颜色位置对** ，用于描述每个环：

- 第 `i` 对中的 **第一个** 字符表示第 `i` 个环的 **颜色**（`'R'`、`'G'`、`'B'`）。
- 第 `i` 对中的 **第二个** 字符表示第 `i` 个环的 **位置**，也就是位于哪根杆上（`'0'` 到 `'9'`）。

例如，`"R3G2B1"` 表示：共有 `n == 3` 个环，红色的环在编号为 3 的杆上，绿色的环在编号为 2 的杆上，蓝色的环在编号为 1 的杆上。

找出所有集齐 **全部三种颜色** 环的杆，并返回这种杆的数量。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/11/23/ex1final.png)

```
输入：rings = "B0B6G0R6R0R6G9"
输出：1
解释：
- 编号 0 的杆上有 3 个环，集齐全部颜色：红、绿、蓝。
- 编号 6 的杆上有 3 个环，但只有红、蓝两种颜色。
- 编号 9 的杆上只有 1 个绿色环。
因此，集齐全部三种颜色环的杆的数目为 1 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/11/23/ex2final.png)

```
输入：rings = "B0R0G0R9R0B0G0"
输出：1
解释：
- 编号 0 的杆上有 6 个环，集齐全部颜色：红、绿、蓝。
- 编号 9 的杆上只有 1 个红色环。
因此，集齐全部三种颜色环的杆的数目为 1 。
```

**示例 3：**

```
输入：rings = "G4"
输出：0
解释：
只给了一个环，因此，不存在集齐全部三种颜色环的杆。
```

 

**提示：**

- `rings.length == 2 * n`
- `1 <= n <= 100`
- 如 `i` 是 **偶数** ，则 `rings[i]` 的值可以取 `'R'`、`'G'` 或 `'B'`（下标从 **0** 开始计数）
- 如 `i` 是 **奇数** ，则 `rings[i]` 的值可以取 `'0'` 到 `'9'` 中的一个数字（下标从 **0** 开始计数）



#### 分析

按照奇数位置分类即可



#### 代码

```java
class Solution {
    public int countPoints(String rings) {
        Map<Integer, Set<Character>> map = new HashMap<>();
        
        for(int i=0;i<rings.length();i += 2) {
            char ring = rings.charAt(i);
            int bar = rings.charAt(i + 1);
            Set<Character> set = map.getOrDefault(bar, new HashSet<>());
            set.add(ring);
            
            map.put(bar, set);
        }
        int result = 0;
        for(Map.Entry<Integer, Set<Character>> entry : map.entrySet()) {
            if(entry.getValue().size() == 3) result++;
        }
        
        return result;
    }
}
```

------

### 题目二、[5953. 子数组范围和](https://leetcode-cn.com/problems/sum-of-subarray-ranges/)【中等】

#### 题目描述

给你一个整数数组 `nums` 。`nums` 中，子数组的 **范围** 是子数组中最大元素和最小元素的差值。

返回 `nums` 中 **所有** 子数组范围的 **和** *。*

子数组是数组中一个连续 **非空** 的元素序列。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：4
解释：nums 的 6 个子数组如下所示：
[1]，范围 = 最大 - 最小 = 1 - 1 = 0 
[2]，范围 = 2 - 2 = 0
[3]，范围 = 3 - 3 = 0
[1,2]，范围 = 2 - 1 = 1
[2,3]，范围 = 3 - 2 = 1
[1,2,3]，范围 = 3 - 1 = 2
所有范围的和是 0 + 0 + 0 + 1 + 1 + 2 = 4
```

**示例 2：**

```
输入：nums = [1,3,3]
输出：4
解释：nums 的 6 个子数组如下所示：
[1]，范围 = 最大 - 最小 = 1 - 1 = 0
[3]，范围 = 3 - 3 = 0
[3]，范围 = 3 - 3 = 0
[1,3]，范围 = 3 - 1 = 2
[3,3]，范围 = 3 - 3 = 0
[1,3,3]，范围 = 3 - 1 = 2
所有范围的和是 0 + 0 + 0 + 2 + 0 + 2 = 4
```

**示例 3：**

```
输入：nums = [4,-2,-3,4,1]
输出：59
解释：nums 中所有子数组范围的和是 59
```

 

**提示：**

- `1 <= nums.length <= 1000`
- `-10^9 <= nums[i] <= 10^9`



#### 分析

本题的nums长度最多是1000，所以可以使用O(n^2)复杂度的算法，用两层循环可以解决。

连续非空序列，第一层循环枚举序列的起点，第二层循环枚举序列的终点。第二层循环内维护当前序列的最大值和最小值。



#### 代码

```java
class Solution {
    public long subArrayRanges(int[] nums) {
        long result = 0l;
        int n = nums.length;
        for(int i=0;i<n;i++) {
            int min = nums[i], max = nums[i];
            for(int j=i + 1;j<n;j++) {
                min = Math.min(min, nums[j]);
                max = Math.max(max, nums[j]);
                
                result += (long) max - (long)min;
            }
        }
        
        return result;
    }
}
```

------

### 题目三、[5954. 给植物浇水 II](https://leetcode-cn.com/problems/watering-plants-ii/)【中等】

#### 题目描述

Alice 和 Bob 打算给花园里的 `n` 株植物浇水。植物排成一行，从左到右进行标记，编号从 `0` 到 `n - 1` 。其中，第 `i` 株植物的位置是 `x = i` 。

每一株植物都需要浇特定量的水。Alice 和 Bob 每人有一个水罐，**最初是满的** 。他们按下面描述的方式完成浇水：

-  Alice 按 **从左到右** 的顺序给植物浇水，从植物 `0` 开始。Bob 按 **从右到左** 的顺序给植物浇水，从植物 `n - 1` 开始。他们 **同时** 给植物浇水。
- 如果没有足够的水 **完全** 浇灌下一株植物，他 / 她会立即重新灌满浇水罐。
- 不管植物需要多少水，浇水所耗费的时间都是一样的。
- **不能** 提前重新灌满水罐。
- 每株植物都可以由 Alice 或者 Bob 来浇水。
- 如果 Alice 和 Bob 到达同一株植物，那么当前水罐中水更多的人会给这株植物浇水。如果他俩水量相同，那么 Alice 会给这株植物浇水。

给你一个下标从 **0** 开始的整数数组 `plants` ，数组由 `n` 个整数组成。其中，`plants[i]` 为第 `i` 株植物需要的水量。另有两个整数 `capacityA` 和 `capacityB` 分别表示 Alice 和 Bob 水罐的容量。返回两人浇灌所有植物过程中重新灌满水罐的 **次数** 。

 

**示例 1：**

```
输入：plants = [2,2,3,3], capacityA = 5, capacityB = 5
输出：1
解释：
- 最初，Alice 和 Bob 的水罐中各有 5 单元水。
- Alice 给植物 0 浇水，Bob 给植物 3 浇水。
- Alice 和 Bob 现在分别剩下 3 单元和 2 单元水。
- Alice 有足够的水给植物 1 ，所以她直接浇水。Bob 的水不够给植物 2 ，所以他先重新装满水，再浇水。
所以，两人浇灌所有植物过程中重新灌满水罐的次数 = 0 + 0 + 1 + 0 = 1 。
```

**示例 2：**

```
输入：plants = [2,2,3,3], capacityA = 3, capacityB = 4
输出：2
解释：
- 最初，Alice 的水罐中有 3 单元水，Bob 的水罐中有 4 单元水。
- Alice 给植物 0 浇水，Bob 给植物 3 浇水。
- Alice 和 Bob 现在都只有 1 单元水，并分别需要给植物 1 和植物 2 浇水。
- 由于他们的水量均不足以浇水，所以他们重新灌满水罐再进行浇水。
所以，两人浇灌所有植物过程中重新灌满水罐的次数 = 0 + 1 + 1 + 0 = 2 。
```

**示例 3：**

```
输入：plants = [5], capacityA = 10, capacityB = 8
输出：0
解释：
- 只有一株植物
- Alice 的水罐有 10 单元水，Bob 的水罐有 8 单元水。因此 Alice 的水罐中水更多，她会给这株植物浇水。
所以，两人浇灌所有植物过程中重新灌满水罐的次数 = 0 。
```

**示例 4：**

```
输入：plants = [1,2,4,4,5], capacityA = 6, capacityB = 5
输出：2
解释：
- 最初，Alice 的水罐中有 6 单元水，Bob 的水罐中有 5 单元水。
- Alice 给植物 0 浇水，Bob 给植物 4 浇水。
- Alice 和 Bob 现在分别剩下 5 单元和 0 单元水。
- Alice 有足够的水给植物 1 ，所以她直接浇水。Bob 的水不够给植物 3 ，所以他先重新装满水，再浇水。
- Alice 和 Bob 现在分别剩下 3 单元和 1 单元水。
- 由于 Alice 的水更多，所以由她给植物 2 浇水。然而，她水罐里的水不够给植物 2 ，所以她先重新装满水，再浇水。 
所以，两人浇灌所有植物过程中重新灌满水罐的次数 = 0 + 0 + 1 + 1 + 0 = 2 。
```

**示例 5：**

```
输入：plants = [2,2,5,2,2], capacityA = 5, capacityB = 5
输出：1
解释：
Alice 和 Bob 都会到达中间的植物，并且此时他俩剩下的水量相同，所以 Alice 会给这株植物浇水。
由于她到达时只剩下 1 单元水，所以需要重新灌满水罐。
这是唯一一次需要重新灌满水罐的情况。所以，两人浇灌所有植物过程中重新灌满水罐的次数 = 1 。
```

 

**提示：**

- `n == plants.length`
- `1 <= n <= 10^5`
- `1 <= plants[i] <= 10^6`
- `max(plants[i]) <= capacityA, capacityB <= 10^9`



#### 分析

模拟题，按照题意进行模拟即可



#### 代码

```java
class Solution {
    public int minimumRefill(int[] plants, int capacityA, int capacityB) {
        int n = plants.length;
        
        int left = 0, right = n - 1;
        int leftWater = capacityA, rightWater = capacityB;
        int result = 0;
        while(left < right) {
            if(leftWater >= plants[left]) {
                leftWater -= plants[left];
            } else {
                result++;
                leftWater = capacityA - plants[left];
            }
            
            if(rightWater >= plants[right]) {
                rightWater -= plants[right];
            } else {
                result++;
                rightWater = capacityB - plants[right];
            }
            
            left++;
            right--;  
        }
        if(left == right) {
            if(Math.max(leftWater, rightWater) < plants[left]) result++;
        }
        
        return result;
    }
}
```

------

### 题目四、[5955. 摘水果](https://leetcode-cn.com/problems/maximum-fruits-harvested-after-at-most-k-steps/)【困难】

#### 题目描述

在一个无限的 x 坐标轴上，有许多水果分布在其中某些位置。给你一个二维整数数组 `fruits` ，其中 `fruits[i] = [positioni, amounti]` 表示共有 `amounti` 个水果放置在 `positioni` 上。`fruits` 已经按 `positioni` **升序排列** ，每个 `positioni` **互不相同** 。

另给你两个整数 `startPos` 和 `k` 。最初，你位于 `startPos` 。从任何位置，你可以选择 **向左或者向右** 走。在 x 轴上每移动 **一个单位** ，就记作 **一步** 。你总共可以走 **最多** `k` 步。你每达到一个位置，都会摘掉全部的水果，水果也将从该位置消失（不会再生）。

返回你可以摘到水果的 **最大总数** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/11/21/1.png)

```
输入：fruits = [[2,8],[6,3],[8,6]], startPos = 5, k = 4
输出：9
解释：
最佳路线为：
- 向右移动到位置 6 ，摘到 3 个水果
- 向右移动到位置 8 ，摘到 6 个水果
移动 3 步，共摘到 3 + 6 = 9 个水果
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/11/21/2.png)

```
输入：fruits = [[0,9],[4,1],[5,7],[6,2],[7,4],[10,9]], startPos = 5, k = 4
输出：14
解释：
可以移动最多 k = 4 步，所以无法到达位置 0 和位置 10 。
最佳路线为：
- 在初始位置 5 ，摘到 7 个水果
- 向左移动到位置 4 ，摘到 1 个水果
- 向右移动到位置 6 ，摘到 2 个水果
- 向右移动到位置 7 ，摘到 4 个水果
移动 1 + 3 = 4 步，共摘到 7 + 1 + 2 + 4 = 14 个水果
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2021/11/21/3.png)

```
输入：fruits = [[0,3],[6,4],[8,5]], startPos = 3, k = 2
输出：0
解释：
最多可以移动 k = 2 步，无法到达任一有水果的地方
```

 

**提示：**

- `1 <= fruits.length <= 10^5`
- `fruits[i].length == 2`
- `0 <= startPos, positioni <= 2 * 10^5`
- 对于任意 `i > 0` ，`positioni-1 < positioni` 均成立（下标从 **0** 开始计数）
- `1 <= amounti <= 10^4`
- `0 <= k <= 2 * 10^5`



#### 分析

本题最优情况是向左走i(0<=i<=k)步然后再向右走k - 2 * i步，结束采摘。如果中间有来回走肯定不是最优的情况。

最优情况示意图：

<img src="/Users/chenbinbin/Library/Application Support/typora-user-images/image-20211212230859300.png" alt="image-20211212230859300" style="zoom:67%;" />

只要枚举l和r的值，并且计算l到r的水果总和的最大值即可。



1,要计算l到r的水果总和，所以要用到前缀和：

```java
int max = 2 * 100000;
int[] preSum = new int[max + 1];
int[] arr = new int[max + 1];
for(int[] fruit : fruits) {
  arr[fruit[0]] = fruit[1];
}

preSum[0] = arr[0];
for(int i=1;i<arr.length;i++) {
  preSum[i] = preSum[i-1] + arr[i];
}
```



2.枚举左端点l的值，l离startPos的距离范围为0到Math.min(startPos, k)：

左端点为l时，右端点r = l + 2 * i

```java
int result = 0;
int l = 0, r = 0;
for(int i=0;i<=Math.min(startPos, k);i++) {
  l = startPos - i;
  r = l + k - i;
  if(l < 0 || r > max) continue;
  result = Math.max(preSum[r] - preSum[l] + arr[l], result);
}
```



3.枚举右端点的值

```java
for(int i=0;i<=Math.min(k, max - startPos);i++) {
  r = startPos + i;
  l = r - k + i;
  if(l < 0) l =0;
  if(l > startPos) l = startPos;
  
  if(l < 0 || r > max) continue;
  
  result = Math.max(preSum[r] - preSum[l] + arr[l], result);
}
```



#### 代码

```java
class Solution {
  public int maxTotalFruits(int[][] fruits, int startPos, int k) {
    //构造前缀和
    int max = 2 * 100000;
    int[] preSum = new int[max + 1];
    int[] arr = new int[max + 1];
    for (int[] fruit : fruits) {
      arr[fruit[0]] = fruit[1];
    }
    preSum[0] = arr[0];
    for (int i = 1; i < arr.length; i++) {
      preSum[i] = preSum[i - 1] + arr[i];
    }
    
    int result = 0;
    int l = 0, r = 0;
    
    //枚举左端点
    for (int i = 0; i <= Math.min(startPos, k); i++) {
      l = startPos - i;
      r = l + k - i;
      if (l < 0 || r > max) continue;
      result = Math.max(preSum[r] - preSum[l] + arr[l], result);
    }
    
    //枚举右端点
    for (int i = 0; i <= Math.min(k, max - startPos); i++) {
      r = startPos + i;
      l = r - k + i;
      if (l < 0) l = 0;
      if (l > startPos) l = startPos;
      if (l < 0 || r > max) continue;
      result = Math.max(preSum[r] - preSum[l] + arr[l], result);
    }
    
    return result;
  }
}
```

