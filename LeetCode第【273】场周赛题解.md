###### **本文主要解析LeetCode在2021年12月26日10：30组织的第【273】场周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/weekly-contest-268)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/chen-xiao-bin-5/)**。**

---

### 题目一、[5963. 反转两次的数字](https://leetcode-cn.com/problems/a-number-after-a-double-reversal/)【简单】

#### 题目描述

**反转** 一个整数意味着倒置它的所有位。

- 例如，反转 `2021` 得到 `1202` 。反转 `12300` 得到 `321` ，**不保留前导零** 。

给你一个整数 `num` ，**反转** `num` 得到 `reversed1` ，**接着反转** `reversed1` 得到 `reversed2` 。如果 `reversed2` 等于 `num` ，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

```
输入：num = 526
输出：true
解释：反转 num 得到 625 ，接着反转 625 得到 526 ，等于 num 。
```

**示例 2：**

```
输入：num = 1800
输出：false
解释：反转 num 得到 81 ，接着反转 81 得到 18 ，不等于 num 。 
```

**示例 3：**

```
输入：num = 0
输出：true
解释：反转 num 得到 0 ，接着反转 0 得到 0 ，等于 num 。
```

 

**提示：**

- `0 <= num <= 10^6`



#### 分析

只要小于10 或者数字末尾不为0就能满足要求。



#### 代码

```python
class Solution(object):
    def isSameAfterReversals(self, num):
        return num < 10 or num % 10 != 0
```



------

### 题目二、[5964. 执行所有后缀指令](https://leetcode-cn.com/problems/execution-of-all-suffix-instructions-staying-in-a-grid/)【中等】

#### 题目描述

现有一个 `n x n` 大小的网格，左上角单元格坐标 `(0, 0)` ，右下角单元格坐标 `(n - 1, n - 1)` 。给你整数 `n` 和一个整数数组 `startPos` ，其中 `startPos = [startrow, startcol]` 表示机器人最开始在坐标为 `(startrow, startcol)` 的单元格上。

另给你一个长度为 `m` 、下标从 **0** 开始的字符串 `s` ，其中 `s[i]` 是对机器人的第 `i` 条指令：`'L'`（向左移动），`'R'`（向右移动），`'U'`（向上移动）和 `'D'`（向下移动）。

机器人可以从 `s` 中的任一第 `i` 条指令开始执行。它将会逐条执行指令直到 `s` 的末尾，但在满足下述条件之一时，机器人将会停止：

- 下一条指令将会导致机器人移动到网格外。
- 没有指令可以执行。

返回一个长度为 `m` 的数组 `answer` ，其中 `answer[i]` 是机器人从第 `i` 条指令 **开始** ，可以执行的 **指令数目** 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/12/09/1.png)

```
输入：n = 3, startPos = [0,1], s = "RRDDLU"
输出：[1,5,4,3,1,0]
解释：机器人从 startPos 出发，并从第 i 条指令开始执行：
- 0: "RRDDLU" 在移动到网格外之前，只能执行一条 "R" 指令。
- 1:  "RDDLU" 可以执行全部五条指令，机器人仍在网格内，最终到达 (0, 0) 。
- 2:   "DDLU" 可以执行全部四条指令，机器人仍在网格内，最终到达 (0, 0) 。
- 3:    "DLU" 可以执行全部三条指令，机器人仍在网格内，最终到达 (0, 0) 。
- 4:     "LU" 在移动到网格外之前，只能执行一条 "L" 指令。
- 5:      "U" 如果向上移动，将会移动到网格外。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/12/09/2.png)

```
输入：n = 2, startPos = [1,1], s = "LURD"
输出：[4,1,0,0]
解释：
- 0: "LURD"
- 1:  "URD"
- 2:   "RD"
- 3:    "D"
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2021/12/09/3.png)

```
输入：n = 1, startPos = [0,0], s = "LRUD"
输出：[0,0,0,0]
解释：无论机器人从哪条指令开始执行，都会移动到网格外。
```

 

**提示：**

- `m == s.length`
- `1 <= n, m <= 500`
- `startPos.length == 2`
- `0 <= startrow, startcol < n`
- `s` 由 `'L'`、`'R'`、`'U'` 和 `'D'` 组成



#### 分析

本题数据量比较小，逐个遍历即可



#### 代码

```Python
class Solution(object):
    def executeInstructions(self, n, startPos, s):
        directions = {
            'L':[0, -1],
            'R':[0, 1],
            'U':[-1, 0],
            'D':[1, 0]
        }

        result = []
        for i in range(0, len(s)):
            x = startPos[0]
            y = startPos[1]
            count = 0

            for j in range(i, len(s)):
                direction = directions[s[j]]
                x += direction[0]
                y += direction[1]
                if(x < 0 or x >= n or y < 0 or y >= n):
                    break
                count += 1
            result.append(count)
        
        return result
            
```

------

### 题目三、[5965. 相同元素的间隔之和](https://leetcode-cn.com/problems/intervals-between-identical-elements/)【中等】

#### 题目描述

给你一个下标从 **0** 开始、由 `n` 个整数组成的数组 `arr` 。

`arr` 中两个元素的 **间隔** 定义为它们下标之间的 **绝对差** 。更正式地，`arr[i]` 和 `arr[j]` 之间的间隔是 `|i - j|` 。

返回一个长度为 `n` 的数组 `intervals` ，其中 `intervals[i]` 是 `arr[i]` 和 `arr` 中每个相同元素（与 `arr[i]` 的值相同）的 **间隔之和** *。*

**注意：**`|x|` 是 `x` 的绝对值。

 

**示例 1：**

```
输入：arr = [2,1,3,1,2,3,3]
输出：[4,2,7,2,4,4,5]
解释：
- 下标 0 ：另一个 2 在下标 4 ，|0 - 4| = 4
- 下标 1 ：另一个 1 在下标 3 ，|1 - 3| = 2
- 下标 2 ：另两个 3 在下标 5 和 6 ，|2 - 5| + |2 - 6| = 7
- 下标 3 ：另一个 1 在下标 1 ，|3 - 1| = 2
- 下标 4 ：另一个 2 在下标 0 ，|4 - 0| = 4
- 下标 5 ：另两个 3 在下标 2 和 6 ，|5 - 2| + |5 - 6| = 4
- 下标 6 ：另两个 3 在下标 2 和 5 ，|6 - 2| + |6 - 5| = 5
```

**示例 2：**

```
输入：arr = [10,5,10,10]
输出：[5,0,3,4]
解释：
- 下标 0 ：另两个 10 在下标 2 和 3 ，|0 - 2| + |0 - 3| = 5
- 下标 1 ：只有这一个 5 在数组中，所以到相同元素的间隔之和是 0
- 下标 2 ：另两个 10 在下标 0 和 3 ，|2 - 0| + |2 - 3| = 3
- 下标 3 ：另两个 10 在下标 0 和 2 ，|3 - 0| + |3 - 2| = 4
```

 

**提示：**

- `n == arr.length`
- `1 <= n <= 10^5`
- `1 <= arr[i] <= 10^5`



#### 分析

1.计算出每个数字的位置下标列表

2.计算列表中每个数字与其他数字的绝对值之差的总和



问题转化成在一个严格递增的列表中求每一个数字与其他所有数字的绝对值之差的总和

假设一个严格递增的数组[a1, a2, a3, a4, a5, a6]， 如果要求a3与其他所有数字的绝对值之差的总和，则有：

sum = |a3 - a1| + |a3 - a2| + |a3 - a4| + |a3 - a5| + |a3 - a6|

因为数组严格递增，则有a3 > a1、a3 > a2、a3 < a4、a3 < a5、a3 < a6

所以去掉绝对值符号后， sum = a3 - a1 + a3 - a2  + a4 - a3 + a5 - a3 + a6 - a3

简化后可得sum = 2 * a3 - (a1 + a2) + (a4 + a5 + a6) - 3 * a3

在经过化简得：sum = 3 * a3 - (a1 + a2 + a3)  + (a4 + a5 + a6) - 3 * a3

a1 + a2 + a3为a3元素之前的前缀和， a4 + a5 + a6为a3之后的后缀和，可以转化为前缀和即：preSum[5] - preSum[2]



所以，一般的，如果要求一个严格递增数组中第i个数与其他所有数字的绝对值之差的总和，则有：

**sum = (i + 1) * nums[i] - preSum[i] + preSum[n - 1] - preSum[i] - (n - 1  - i) * nums[i]** 



java代码小心整数溢出。

#### 代码

```java
class Solution {
    long[] result;
    public long[] getDistances(int[] arr) {
        int n = arr.length;
        result = new long[n];
        Map<Integer, List<Integer>> map = new HashMap<>();
        
        for(int i=0;i<n;i++) {
            List<Integer> list = map.getOrDefault(arr[i], new ArrayList<>());
            list.add(i);
            map.put(arr[i], list);
        }
        
        for(Map.Entry<Integer, List<Integer>> entry : map.entrySet()) {
            List<Integer> list = entry.getValue();
            handle(list);
        }
        
        return result;
    }
    
    
    private void handle(List<Integer> list) {
        int n = list.size();
        long[] preSum = new long[n];
        preSum[0] = list.get(0);
        
        for(int i=1;i<list.size();i++) {
            preSum[i] = preSum[i-1] + list.get(i);
        }
        
        for(int i=0;i<n;i++) {
            int num = list.get(i);
            long val = (long)(i+1)*(long)list.get(i)-preSum[i]+ preSum[n-1]-preSum[i]-(long)list.get(i)*(long)(n-1-i);
            result[num] = val;
        }
    }
}
```

------

### 题目四、[5966. 还原原数组](https://leetcode-cn.com/problems/recover-the-original-array/)【困难】

#### 题目描述

Alice 有一个下标从 **0** 开始的数组 `arr` ，由 `n` 个正整数组成。她会选择一个任意的 **正整数** `k` 并按下述方式创建两个下标从 **0** 开始的新整数数组 `lower` 和 `higher` ：

1. 对每个满足 `0 <= i < n` 的下标 `i` ，`lower[i] = arr[i] - k`
2. 对每个满足 `0 <= i < n` 的下标 `i` ，`higher[i] = arr[i] + k`

不幸地是，Alice 丢失了全部三个数组。但是，她记住了在数组 `lower` 和 `higher` 中出现的整数，但不知道每个整数属于哪个数组。请你帮助 Alice 还原原数组。

给你一个由 2n 个整数组成的整数数组 `nums` ，其中 **恰好** `n` 个整数出现在 `lower` ，剩下的出现在 `higher` ，还原并返回 **原数组** `arr` 。如果出现答案不唯一的情况，返回 **任一** 有效数组。

**注意：**生成的测试用例保证存在 **至少一个** 有效数组 `arr` 。

 

**示例 1：**

```
输入：nums = [2,10,6,4,8,12]
输出：[3,7,11]
解释：
如果 arr = [3,7,11] 且 k = 1 ，那么 lower = [2,6,10] 且 higher = [4,8,12] 。
组合 lower 和 higher 得到 [2,6,10,4,8,12] ，这是 nums 的一个排列。
另一个有效的数组是 arr = [5,7,9] 且 k = 3 。在这种情况下，lower = [2,4,6] 且 higher = [8,10,12] 。
```

**示例 2：**

```
输入：nums = [1,1,3,3]
输出：[2,2]
解释：
如果 arr = [2,2] 且 k = 1 ，那么 lower = [1,1] 且 higher = [3,3] 。
组合 lower 和 higher 得到 [1,1,3,3] ，这是 nums 的一个排列。
注意，数组不能是 [1,3] ，因为在这种情况下，获得 [1,1,3,3] 唯一可行的方案是 k = 0 。
这种方案是无效的，k 必须是一个正整数。
```

**示例 3：**

```
输入：nums = [5,435]
输出：[220]
解释：
唯一可行的组合是 arr = [220] 且 k = 215 。在这种情况下，lower = [5] 且 higher = [435] 。
```

 

**提示：**

- `2 * n == nums.length`
- `1 <= n <= 1000`
- `1 <= nums[i] <= 10^9`
- 生成的测试用例保证存在 **至少一个** 有效数组 `arr`



#### 分析

本题分成两个步骤求解：

1.求出k

2.构造原数组



由于本题的数据量比较小，所以可以枚举k进行尝试，如果成功，则直接返回：

由于数组中的最大值肯定是处于higher数组，所以可以通过枚举数组最大值max与数组中的其他值的差除以2作为k进行尝试；



构造数组，由于最小值肯定是处于lower数组，所以可以每次取数组中的最小值进行构造数组。如果能成功构造数组，则当前的k是满足题意的。如果不能成功构造数组，则遍历下一个k。



#### 代码

```java
class Solution {
  public int[] recoverArray(int[] nums) {
    int n = nums.length / 2;
    Arrays.sort(nums);
    int[] result = new int[n];
    
    for(int p=2 * n - 2; p>=0; p--) {
      if(nums[2 * n - 1] == nums[p] || (nums[2 * n - 1] - nums[p]) % 2 !=0) continue;
      int k = (nums[2 * n - 1] - nums[p]) / 2;
      
      TreeMap<Integer, Integer> numMap = new TreeMap<>();
      for(int num : nums) {
        int count = numMap.getOrDefault(num, 0) + 1;
        numMap.put(num, count);
      }
      
      result = new int[n];
      boolean flag = true;
      for(int i=0;i<n;i++) {
        int num = numMap.firstKey();
        result[i] = num + k;
        int count = numMap.get(num) - 1;
        if(count == 0) {
          numMap.remove(num);
        } else {
          numMap.put(num, count);
        }
        
        if(!numMap.containsKey(num + 2 * k)) {
          flag = false;
          break;
        }
        
        count = numMap.get(num + 2 * k) - 1;
        if(count == 0) {
          numMap.remove(num + 2 * k);
        } else {
          numMap.put(num + 2 * k, count);
        }
      }
      
      if(flag) return result;
    }
    
    return result;
  }
}
```

