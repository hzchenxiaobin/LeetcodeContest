### 题目一、[5980. 将字符串拆分为若干长度为 k 的组](https://leetcode-cn.com/problems/divide-a-string-into-groups-of-size-k/)【简单】

字符串 `s` 可以按下述步骤划分为若干长度为 `k` 的组：

- 第一组由字符串中的前 `k` 个字符组成，第二组由接下来的 `k` 个字符串组成，依此类推。每个字符都能够成为 **某一个** 组的一部分。
- 对于最后一组，如果字符串剩下的字符 **不足** `k` 个，需使用字符 `fill` 来补全这一组字符。

注意，在去除最后一个组的填充字符 `fill`（如果存在的话）并按顺序连接所有的组后，所得到的字符串应该是 `s` 。

给你一个字符串 `s` ，以及每组的长度 `k` 和一个用于填充的字符 `fill` ，按上述步骤处理之后，返回一个字符串数组，该数组表示 `s` 分组后 **每个组的组成情况** 。

 

**示例 1：**

```
输入：s = "abcdefghi", k = 3, fill = "x"
输出：["abc","def","ghi"]
解释：
前 3 个字符是 "abc" ，形成第一组。
接下来 3 个字符是 "def" ，形成第二组。
最后 3 个字符是 "ghi" ，形成第三组。
由于所有组都可以由字符串中的字符完全填充，所以不需要使用填充字符。
因此，形成 3 组，分别是 "abc"、"def" 和 "ghi" 。
```

**示例 2：**

```
输入：s = "abcdefghij", k = 3, fill = "x"
输出：["abc","def","ghi","jxx"]
解释：
与前一个例子类似，形成前三组 "abc"、"def" 和 "ghi" 。
对于最后一组，字符串中仅剩下字符 'j' 可以用。为了补全这一组，使用填充字符 'x' 两次。
因此，形成 4 组，分别是 "abc"、"def"、"ghi" 和 "jxx" 。
```

 

**提示：**

- `1 <= s.length <= 100`
- `s` 仅由小写英文字母组成
- `1 <= k <= 100`
- `fill` 是一个小写英文字母



#### 分析

本题是一道简单题，直接模拟即可。



#### 代码

```java
class Solution {
  public String[] divideString(String s, int k, char fill) {
    int n = s.length();
    int p = n / k;
    if(n % k != 0) p++;
    String[] result = new String[p];
    int index = 0, ri = 0;
    for(int i=0;i<p;i++) {
        StringBuilder sb = new StringBuilder();
        for(int j=0;j<k;j++) {
            if(index < n) {
                sb.append(s.charAt(index++));
            } else {
                sb.append(fill);
            }
        }
        result[ri++] = sb.toString();
    }
    
    return result;
  }
}
```

------

### 题目二、[5194. 得到目标值的最少行动次数](https://leetcode-cn.com/problems/minimum-moves-to-reach-target-score/)【中等】

你正在玩一个整数游戏。从整数 `1` 开始，期望得到整数 `target` 。

在一次行动中，你可以做下述两种操作之一：

- **递增**，将当前整数的值加 1（即， `x = x + 1`）。
- **加倍**，使当前整数的值翻倍（即，`x = 2 * x`）。

在整个游戏过程中，你可以使用 **递增** 操作 **任意** 次数。但是只能使用 **加倍** 操作 **至多** `maxDoubles` 次。

给你两个整数 `target` 和 `maxDoubles` ，返回从 1 开始得到 `target` 需要的最少行动次数。

 

**示例 1：**

```
输入：target = 5, maxDoubles = 0
输出：4
解释：一直递增 1 直到得到 target 。
```

**示例 2：**

```
输入：target = 19, maxDoubles = 2
输出：7
解释：最初，x = 1 。
递增 3 次，x = 4 。
加倍 1 次，x = 8 。
递增 1 次，x = 9 。
加倍 1 次，x = 18 。
递增 1 次，x = 19 。
```

**示例 3：**

```
输入：target = 10, maxDoubles = 4
输出：4
解释：
最初，x = 1 。 
递增 1 次，x = 2 。 
加倍 1 次，x = 4 。 
递增 1 次，x = 5 。 
加倍 1 次，x = 10 。 
```

 

**提示：**

- `1 <= target <= 10^9`
- `0 <= maxDoubles <= 100`



#### 分析

假设游戏中没有加倍操作，只有递增操作，那么需要需要操作的次数就是target - 1。

我们再来分析加倍操作，假设对p进行加倍操作，从p -> 2p，那么操作次数就减少了p - 1次(减1是因为加倍需要一次操作)，即总操作次数为target - 1 - (p - 1)次，p值越大，总操作次数越小。所以最少操作次数为：

target - 1 - (target / 2 - 1) - (target / 4 - 1) -...



#### 代码

```java
class Solution {
    public int minMoves(int target, int maxDoubles) {
        int count = target - 1;
        while(target >= 2 && maxDoubles > 0) {
            maxDoubles -= 1;
            count -= target / 2 - 1;
            target /= 2;
        }
        return count;  
    }
}
```

------

### 题目三、[5982. 解决智力问题](https://leetcode-cn.com/problems/solving-questions-with-brainpower/)【中等】

给你一个下标从 **0** 开始的二维整数数组 `questions` ，其中 `questions[i] = [pointsi, brainpoweri]` 。

这个数组表示一场考试里的一系列题目，你需要 **按顺序** （也就是从问题 `0` 开始依次解决），针对每个问题选择 **解决** 或者 **跳过** 操作。解决问题 `i` 将让你 **获得** `pointsi` 的分数，但是你将 **无法** 解决接下来的 `brainpoweri` 个问题（即只能跳过接下来的 `brainpoweri` 个问题）。如果你跳过问题 `i` ，你可以对下一个问题决定使用哪种操作。

- 比方说，给你 

  ```
  questions = [[3, 2], [4, 3], [4, 4], [2, 5]]
  ```

   ：

  - 如果问题 `0` 被解决了， 那么你可以获得 `3` 分，但你不能解决问题 `1` 和 `2` 。
  - 如果你跳过问题 `0` ，且解决问题 `1` ，你将获得 `4` 分但是不能解决问题 `2` 和 `3` 。

请你返回这场考试里你能获得的 **最高** 分数。

 

**示例 1：**

```
输入：questions = [[3,2],[4,3],[4,4],[2,5]]
输出：5
解释：解决问题 0 和 3 得到最高分。
- 解决问题 0 ：获得 3 分，但接下来 2 个问题都不能解决。
- 不能解决问题 1 和 2
- 解决问题 3 ：获得 2 分
总得分为：3 + 2 = 5 。没有别的办法获得 5 分或者多于 5 分。
```

**示例 2：**

```
输入：questions = [[1,1],[2,2],[3,3],[4,4],[5,5]]
输出：7
解释：解决问题 1 和 4 得到最高分。
- 跳过问题 0
- 解决问题 1 ：获得 2 分，但接下来 2 个问题都不能解决。
- 不能解决问题 2 和 3
- 解决问题 4 ：获得 5 分
总得分为：2 + 5 = 7 。没有别的办法获得 7 分或者多于 7 分。
```

 

**提示：**

- `1 <= questions.length <= 10^5`
- `questions[i].length == 2`
- `1 <= pointsi, brainpoweri <= 10^5`



#### 分析

从前向后DP

定义dp[i]表示区间[0,i]内可以获得的最高分数，那么

若跳过i，则dp[i + 1] = Math.max(dp[i], dp[i+1])

若解决i，则dp[i + brainpower + 1] = Math.max(dp[i] + point, dp[i + brainpower + 1])



#### 代码

```java
class Solution {
    public long mostPoints(int[][] questions) {
        int n = questions.length;
        long[] dp = new long[n + 1];
        long res = 0;
        
        for(int i=0;i<n;i++) {
            int point = questions[i][0];
            int brainpower = questions[i][1];
            if(i + 1 <= n) dp[i+1] = Math.max(dp[i], dp[i+1]);
            int next = Math.min(i + brainpower + 1, n);
            if(next <= n) dp[next] = Math.max(dp[next], dp[i] + point);
        }
        
        return dp[n];
    }
}
```

------

### 题目四、[5983. 同时运行 N 台电脑的最长时间](https://leetcode-cn.com/problems/maximum-running-time-of-n-computers/)【困难】

你有 `n` 台电脑。给你整数 `n` 和一个下标从 **0** 开始的整数数组 `batteries` ，其中第 `i` 个电池可以让一台电脑 **运行** `batteries[i]` 分钟。你想使用这些电池让 **全部** `n` 台电脑 **同时** 运行。

一开始，你可以给每台电脑连接 **至多一个电池** 。然后在任意整数时刻，你都可以将一台电脑与它的电池断开连接，并连接另一个电池，你可以进行这个操作 **任意次** 。新连接的电池可以是一个全新的电池，也可以是别的电脑用过的电池。断开连接和连接新的电池不会花费任何时间。

注意，你不能给电池充电。

请你返回你可以让 `n` 台电脑同时运行的 **最长** 分钟数。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2022/01/06/example1-fit.png)

```
输入：n = 2, batteries = [3,3,3]
输出：4
解释：
一开始，将第一台电脑与电池 0 连接，第二台电脑与电池 1 连接。
2 分钟后，将第二台电脑与电池 1 断开连接，并连接电池 2 。注意，电池 0 还可以供电 1 分钟。
在第 3 分钟结尾，你需要将第一台电脑与电池 0 断开连接，然后连接电池 1 。
在第 4 分钟结尾，电池 1 也被耗尽，第一台电脑无法继续运行。
我们最多能同时让两台电脑同时运行 4 分钟，所以我们返回 4 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2022/01/06/example2.png)

```
输入：n = 2, batteries = [1,1,1,1]
输出：2
解释：
一开始，将第一台电脑与电池 0 连接，第二台电脑与电池 2 连接。
一分钟后，电池 0 和电池 2 同时耗尽，所以你需要将它们断开连接，并将电池 1 和第一台电脑连接，电池 3 和第二台电脑连接。
1 分钟后，电池 1 和电池 3 也耗尽了，所以两台电脑都无法继续运行。
我们最多能让两台电脑同时运行 2 分钟，所以我们返回 2 。
```

 

**提示：**

- `1 <= n <= batteries.length <= 10^5`
- `1 <= batteries[i] <= 10^9`



#### 分析

二分法

假设sum为batteries数组的总和， t为所有电脑同时运行的时间，则t的最大值为 sum / n, 最小值是1。通过二分求满足题意的最大值。



判断一段电池能不能支撑所有的电脑同时运行时间t，如果有一块电池的时长超过t，则其最长能够运行的时间就为t，如果所有电池的运行时间加起来大于等于 t * n，则电池能够支撑所有电脑运行t时间。

```java
private boolean check(long t, int n, int[] batteries) {
  long sum = 0L;
  for(int battery : batteries) {
    sum += Math.min(battery, t);
  }
  
  return sum >= t * n;
}
```



#### 代码

```java
class Solution {
    public long maxRunTime(int n, int[] batteries) {
        long sum = 0L;
        for(int battery : batteries) {
            sum += battery;
        }

        long l = 1L, r = sum / n;
        while(l < r) {
            long mid = l + (r - l) / 2;
            boolean check = check(mid, n, batteries);
            if(check) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }
        if(check(l, n, batteries)) return l;
        return l - 1;
    }

    private boolean check(long t, int n, int[] batteries) {
        long sum = 0L;
        for(int battery : batteries) {
            sum += Math.min(battery, t);
        }

        return sum >= t * n;
    }
}
```

