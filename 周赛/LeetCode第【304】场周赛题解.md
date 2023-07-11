### 题目一、[6132. 使数组中所有元素都等于零](https://leetcode.cn/problems/make-array-zero-by-subtracting-equal-amounts/)【简单】

给你一个非负整数数组 `nums` 。在一步操作中，你必须：

- 选出一个正整数 `x` ，`x` 需要小于或等于 `nums` 中 **最小** 的 **非零** 元素。
- `nums` 中的每个正整数都减去 `x`。

返回使 `nums` 中所有元素都等于 `0` 需要的 **最少** 操作数。

 

**示例 1：**

```
输入：nums = [1,5,0,3,5]
输出：3
解释：
第一步操作：选出 x = 1 ，之后 nums = [0,4,0,2,4] 。
第二步操作：选出 x = 2 ，之后 nums = [0,2,0,0,2] 。
第三步操作：选出 x = 2 ，之后 nums = [0,0,0,0,0] 。
```

**示例 2：**

```
输入：nums = [0]
输出：0
解释：nums 中的每个元素都已经是 0 ，所以不需要执行任何操作。
```

 

**提示：**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 100`



### 分析

题目的本质是求非0不同元素的个数，直接模拟即可。



### 代码

```java
class Solution {
    public int minimumOperations(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int num : nums) set.add(num);
        set.remove(0);
        return set.size();
    }
}
```

------

### 题目二、[6133. 分组的最大数量](https://leetcode.cn/problems/maximum-number-of-groups-entering-a-competition/)【中等】

给你一个正整数数组 `grades` ，表示大学中一些学生的成绩。你打算将 **所有** 学生分为一些 **有序** 的非空分组，其中分组间的顺序满足以下全部条件：

- 第 `i` 个分组中的学生总成绩 **小于** 第 `(i + 1)` 个分组中的学生总成绩，对所有组均成立（除了最后一组）。
- 第 `i` 个分组中的学生总数 **小于** 第 `(i + 1)` 个分组中的学生总数，对所有组均成立（除了最后一组）。

返回可以形成的 **最大** 组数。

 

**示例 1：**

```
输入：grades = [10,6,12,7,3,5]
输出：3
解释：下面是形成 3 个分组的一种可行方法：
- 第 1 个分组的学生成绩为 grades = [12] ，总成绩：12 ，学生数：1
- 第 2 个分组的学生成绩为 grades = [6,7] ，总成绩：6 + 7 = 13 ，学生数：2
- 第 3 个分组的学生成绩为 grades = [10,3,5] ，总成绩：10 + 3 + 5 = 18 ，学生数：3 
可以证明无法形成超过 3 个分组。
```

**示例 2：**

```
输入：grades = [8,8]
输出：1
解释：只能形成 1 个分组，因为如果要形成 2 个分组的话，会导致每个分组中的学生数目相等。
```

 

**提示：**

- `1 <= grades.length <= 10^5`
- `1 <= grades[i] <= 10^5`



### 分析

本题的例子比较有迷惑性，看上去比较难，纯贪心的做法。

> 第 `i` 个分组中的学生总数 **小于** 第 `(i + 1)` 个分组中的学生总数

很容易想到将所有的学生分为1个、2个、3个的形式。

> 第 `i` 个分组中的学生总成绩 **小于** 第 `(i + 1)` 个分组中的学生总成绩

将学生按照成绩由低到高排序，然后再将学生分成1个、2个、3个的形式，就能够满足两个条件了。



比如例子1

输入：grades = [10,6,12,7,3,5]

按照成绩排序：[3, 5, 6, 7, 10, 12]

按照学生个数分组:[3], [5, 6], [7,10,12]

所以最大分组个数是3个。



所以只要将grades的元素分成1个、2个、3个....的分组即可，如果多余的元素不够分成新的一组就合并到上一组，不需要关注grades的具体值。



### 代码

```java
class Solution {
    public int maximumGroups(int[] grades) {
        int length=1, n = grades.length;
        int res = 0;
        while(n >= length) {
            res++;
            n-=length;
            length++;
        }
        
        return res;
    }
}
```



也可以通过速算得出结果：

1 + 2 + 3 + ... + n = grades.length

得出： n = Math.sqrt(2 * grades.length + 0.25) - 0.5

```java
class Solution {
    public int maximumGroups(int[] grades) {
        return (int) (Math.sqrt(2 * grades.length + 0.25) - 0.5);
    }
}
```

------

### 题目三、[6134. 找到离给定两个节点最近的节点](https://leetcode.cn/problems/find-closest-node-to-given-two-nodes/)【中等】

给你一个 `n` 个节点的 **有向图** ，节点编号为 `0` 到 `n - 1` ，每个节点 **至多** 有一条出边。

有向图用大小为 `n` 下标从 **0** 开始的数组 `edges` 表示，表示节点 `i` 有一条有向边指向 `edges[i]` 。如果节点 `i` 没有出边，那么 `edges[i] == -1` 。

同时给你两个节点 `node1` 和 `node2` 。

请你返回一个从 `node1` 和 `node2` 都能到达节点的编号，使节点 `node1` 和节点 `node2` 到这个节点的距离 **较大值最小化**。如果有多个答案，请返回 **最小** 的节点编号。如果答案不存在，返回 `-1` 。

注意 `edges` 可能包含环。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-2.png)

```
输入：edges = [2,2,3,-1], node1 = 0, node2 = 1
输出：2
解释：从节点 0 到节点 2 的距离为 1 ，从节点 1 到节点 2 的距离为 1 。
两个距离的较大值为 1 。我们无法得到一个比 1 更小的较大值，所以我们返回节点 2 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-4.png)

```
输入：edges = [1,2,-1], node1 = 0, node2 = 2
输出：2
解释：节点 0 到节点 2 的距离为 2 ，节点 2 到它自己的距离为 0 。
两个距离的较大值为 2 。我们无法得到一个比 2 更小的较大值，所以我们返回节点 2 。
```

 

**提示：**

- `n == edges.length`
- `2 <= n <= 10^5`
- `-1 <= edges[i] < n`
- `edges[i] != i`
- `0 <= node1, node2 < n`



### 分析

1.使用数组记录node1和node2到能到达节点的距离；

2.遍历数组，如果node1和node2都能够到达节点i，则计算距离较大值最小值并记录节点i。



环的判断：

距离数组使用Integer类型，如果d1[i]  != null，则表示已经处理过一次，不再处理。



### 代码

```java
class Solution {

    public int closestMeetingNode(int[] edges, int node1, int node2) {
        int n = edges.length;
        Integer[] d1 = new Integer[n], d2 = new Integer[n];
      
        for (int i = 0; node1 >= 0 && d1[node1] == null; node1 = edges[node1]) {
            d1[node1] = i++;
        }

        for (int i = 0; node2 >= 0 && d2[node2] == null; node2 = edges[node2]) {
            d2[node2] = i++;
        }

        int minDis = Integer.MAX_VALUE, res = -1;
        for (int i = 0; i < n; i++) {
            if (d1[i] == null || d2[i] == null) continue;
            int maxDis = Math.max(d1[i], d2[i]);
            if (maxDis < minDis) {
                minDis = maxDis;
                res = i;
            }

        }
        return res;
    }
}
```

------

### 题目四、[6135. 图中的最长环](https://leetcode.cn/problems/longest-cycle-in-a-graph/)【困难】

给你一个 `n` 个节点的 **有向图** ，节点编号为 `0` 到 `n - 1` ，其中每个节点 **至多** 有一条出边。

图用一个大小为 `n` 下标从 **0** 开始的数组 `edges` 表示，节点 `i` 到节点 `edges[i]` 之间有一条有向边。如果节点 `i` 没有出边，那么 `edges[i] == -1` 。

请你返回图中的 **最长** 环，如果没有任何环，请返回 `-1` 。

一个环指的是起点和终点是 **同一个** 节点的路径。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2022/06/08/graph4drawio-5.png)

```
输入：edges = [3,3,4,2,3]
输出去：3
解释：图中的最长环是：2 -> 4 -> 3 -> 2 。
这个环的长度为 3 ，所以返回 3 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2022/06/07/graph4drawio-1.png)

```
输入：edges = [2,-1,3,1]
输出：-1
解释：图中没有任何环。
```

 

**提示：**

- `n == edges.length`
- `2 <= n <= 10^5`
- `-1 <= edges[i] < n`
- `edges[i] != i`



### 分析

1.使用拓扑排序标记不会形成环的点。

![image-20220731233517633](/Users/chenbinbin/Library/Application Support/typora-user-images/image-20220731233517633.png)

2.计算每个环的节点个数，返回最大环的节点个数。



### 代码

```java
import java.util.LinkedList;
import java.util.Queue;

class Solution {
    boolean[] visited;

    public int longestCycle(int[] edges) {
        int n = edges.length;
        visited = new boolean[n];

        // 拓扑排序标记没有形成环的节点
        topoSort(edges);
        
        int res = -1;
        for (int i = 0; i < n; i++) {
            if (visited[i]) continue;
            int count = 0;
            int next = i;
            // 计算每个环的节点数量
            while (!visited[next]) {
                visited[next] = true;
                next = edges[next];
                count++;
            }
            res = Math.max(res, count);
        }

        return res;
    }

    private void topoSort(int[] edges) {
        int n = edges.length;
        int[] arr = new int[n];
        for (int num : edges) {
            if (num != -1) arr[num]++;
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (arr[i] == 0) queue.offer(i);
        }
        while (!queue.isEmpty()) {
            int t = queue.poll();
            visited[t] = true;
            int next = edges[t];
            if (next == -1) continue;
            arr[next]--;
            if (arr[next] == 0) queue.offer(next);
        }
    }
}
```

