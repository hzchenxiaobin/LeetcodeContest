###### 本文主要解析LeetCode在2021年12月5日10：30组织的第【270】场周赛题目，[竞赛链接](https://leetcode-cn.com/contest/weekly-contest-270)。

###### 有兴趣的同学可以关注一下我的LeetCode[个人账号](https://leetcode-cn.com/u/chen-xiao-bin-5/)。

###### 周赛群人数过多，只能通过邀请进群，有兴趣一起打周赛的同学可以添加我的微信号：cbbdwx，拉你进群

------

### 题目一、[5942. 找出 3 位偶数](https://leetcode-cn.com/problems/finding-3-digit-even-numbers/)【简单】

给你一个整数数组 `digits` ，其中每个元素是一个数字（`0 - 9`）。数组中可能存在重复元素。

你需要找出 **所有** 满足下述条件且 **互不相同** 的整数：

- 该整数由 `digits` 中的三个元素按 **任意** 顺序 **依次连接** 组成。
- 该整数不含 **前导零**
- 该整数是一个 **偶数**

例如，给定的 `digits` 是 `[1, 2, 3]` ，整数 `132` 和 `312` 满足上面列出的全部条件。

将找出的所有互不相同的整数按 **递增顺序** 排列，并以数组形式返回*。*

 

**示例 1：**

```
输入：digits = [2,1,3,0]
输出：[102,120,130,132,210,230,302,310,312,320]
解释：
所有满足题目条件的整数都在输出数组中列出。 
注意，答案数组中不含有 奇数 或带 前导零 的整数。
```

**示例 2：**

```
输入：digits = [2,2,8,8,2]
输出：[222,228,282,288,822,828,882]
解释：
同样的数字（0 - 9）在构造整数时可以重复多次，重复次数最多与其在 digits 中出现的次数一样。 
在这个例子中，数字 8 在构造 288、828 和 882 时都重复了两次。 
```

**示例 3：**

```
输入：digits = [3,7,5]
输出：[]
解释：
使用给定的 digits 无法构造偶数。
```

**示例 4：**

```
输入：digits = [0,2,0,0]
输出：[200]
解释：
唯一一个不含 前导零 且满足全部条件的整数是 200 。
```

**示例 5：**

```
输入：digits = [0,0,0]
输出：[]
解释：
构造的所有整数都会有 前导零 。因此，不存在满足题目条件的整数。
```

 

**提示：**

- `3 <= digits.length <= 100`
- `0 <= digits[i] <= 9`



#### 分析

本题属于简单题

三个for循环分别找出所有满足题意的值



#### 代码

```java
class Solution {
  public int[] findEvenNumbers(int[] digits) {
    //题目要求不重复且有序，所以用TreeSet
    TreeSet<Integer> set = new TreeSet<>();
    
    //for循环找到所有满足题意的值
    int n = digits.length;
    for (int i = 0; i < n; i++) {
      //不能有前导0
      if (digits[i] == 0) continue;
      for (int j = 0; j < n; j++) {
        if (j == i) continue;
        for (int k = 0; k < n; k++) {
          //最后一个数字必须是偶数
          if (k == i || k == j || digits[k] % 2 != 0) continue;
          set.add(digits[i] * 100 + digits[j] * 10 + digits[k]);
        }
      }
    }
    
    //构建返回值
    int size = set.size();
    int index = 0;
    int[] result = new int[size];
    for (int num : set) {
      result[index++] = num;
    }
    
    return result;
  }
}
```

------

### 题目二、[5943. 删除链表的中间节点](https://leetcode-cn.com/problems/delete-the-middle-node-of-a-linked-list/)【中等】

#### 题目描述

给你一个链表的头节点 `head` 。**删除** 链表的 **中间节点** ，并返回修改后的链表的头节点 `head` 。

长度为 `n` 链表的中间节点是从头数起第 `⌊n / 2⌋` 个节点（下标从 **0** 开始），其中 `⌊x⌋` 表示小于或等于 `x` 的最大整数。

- 对于 `n` = `1`、`2`、`3`、`4` 和 `5` 的情况，中间节点的下标分别是 `0`、`1`、`1`、`2` 和 `2` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/11/16/eg1drawio.png)

```
输入：head = [1,3,4,7,1,2,6]
输出：[1,3,4,1,2,6]
解释：
上图表示给出的链表。节点的下标分别标注在每个节点的下方。
由于 n = 7 ，值为 7 的节点 3 是中间节点，用红色标注。
返回结果为移除节点后的新链表。 
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/11/16/eg2drawio.png)

```
输入：head = [1,2,3,4]
输出：[1,2,4]
解释：
上图表示给出的链表。
对于 n = 4 ，值为 3 的节点 2 是中间节点，用红色标注。
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2021/11/16/eg3drawio.png)

```
输入：head = [2,1]
输出：[2]
解释：
上图表示给出的链表。
对于 n = 2 ，值为 1 的节点 1 是中间节点，用红色标注。
值为 2 的节点 0 是移除节点 1 后剩下的唯一一个节点。
```

 

**提示：**

- 链表中节点的数目在范围 `[1, 10^5]` 内
- `1 <= Node.val <= 10^5`



#### 分析

本题的题意可以简化成删除链表中指定位置的节点，解题步骤：

1.找到“中间位置”的的索引

2.删除指定索引的节点



```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
  public ListNode deleteMiddle(ListNode head) {
    //如果只有一个节点，那么应该删除了
    if(head.next == null) return null;
    
    //找到需要删除的节点的索引
    int length = 0;
    ListNode node = head;
    while(node != null) {
      length++;
      node = node.next;
    }
    int delete = length / 2;
    
    //删除指定位置的索引
    node = head;
    int index = 0;
    while(node != null) {
      index++;
      if(index == delete) {
        node.next = node.next.next;
        return head;
      }
      node = node.next;
    }
    
    return null; 
  }
}
```

------

### 题目三、[5944. 从二叉树一个节点到另一个节点每一步的方向](https://leetcode-cn.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another/)【中等】

#### 题目描述

给你一棵 **二叉树** 的根节点 `root` ，这棵二叉树总共有 `n` 个节点。每个节点的值为 `1` 到 `n` 中的一个整数，且互不相同。给你一个整数 `startValue` ，表示起点节点 `s` 的值，和另一个不同的整数 `destValue` ，表示终点节点 `t` 的值。

请找到从节点 `s` 到节点 `t` 的 **最短路径** ，并以字符串的形式返回每一步的方向。每一步用 **大写** 字母 `'L'` ，`'R'` 和 `'U'` 分别表示一种方向：

- `'L'` 表示从一个节点前往它的 **左孩子** 节点。
- `'R'` 表示从一个节点前往它的 **右孩子** 节点。
- `'U'` 表示从一个节点前往它的 **父** 节点。

请你返回从 `s` 到 `t` **最短路径** 每一步的方向。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/11/15/eg1.png)

```
输入：root = [5,1,2,3,null,6,4], startValue = 3, destValue = 6
输出："UURL"
解释：最短路径为：3 → 1 → 5 → 2 → 6 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/11/15/eg2.png)

```
输入：root = [2,1], startValue = 2, destValue = 1
输出："L"
解释：最短路径为：2 → 1 。
```

 

**提示：**

- 树中节点数目为 `n` 。

- `2 <= n <= 10^5`

- `1 <= Node.val <= n`

- 树中所有节点的值 **互不相同** 。

- `1 <= startValue, destValue <= n`

- `startValue != destValue`

  

#### 分析

本题算是一道经典的题目了，经常在竞赛题目中出现。



总结一下这类题目的特点就是：由当前状态到下一个状态的路径是有限的，并且下一个状态跟上一个状态无关。

比如这道题，当前状态到下一个状态，有三种路径，分别是左子节点、右子节点和父节点。



通常的解决方案有：

1.若是求路径长度，那么采用BFS，比如：第63场双周赛的第三题：[2039. 网络空闲的时刻](https://leetcode-cn.com/problems/the-time-when-the-network-becomes-idle/)和263场周赛的第四题：[2045. 到达目的地的第二短时间](https://leetcode-cn.com/problems/second-minimum-time-to-reach-destination/)

2.若是要求具体的路径，那么采用DFS，比如本题。



本题的解题步骤：

1.先求出每一个节点的父节点，存放在map中。

2.通过回溯求出所有从开始节点到达目的节点的路径，取最短的那个。回溯的时候有三种情况，分别是左子节点、右子节点、父节点。



#### 代码

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
  
  Map<Integer, TreeNode> fatherMap = new HashMap<>();
  TreeNode startNode = null;
  String result = "";
  
  public String getDirections(TreeNode root, int startValue, int destValue) {
    //1.获取每个节点的父节点，以及获取开始节点
    dfs(root, startValue);
    
    //2.通过回溯获取所有从开始节点到目标节点的路径
    backTrace(startNode, destValue, new StringBuilder(), new HashSet<>());
    
    //3.返回结果
    return result;  
  }
  
  private void backTrace(TreeNode root,int destValue, StringBuilder sb, Set<Integer> visited) {
    if(root.val == destValue) {
      if(result.length() == 0 || sb.length() < result.length()) result = sb.toString();
      return;
    }
    
    //左子节点
    if(root.left != null && !visited.contains(root.left.val)) {
      visited.add(root.left.val);
      sb.append('L');
      backTrace(root.left, destValue, sb, visited);
      visited.remove(root.left.val);
      sb.deleteCharAt(sb.length() - 1);
    }
    
    //右子节点
    if(root.right != null && !visited.contains(root.right.val)) {
      visited.add(root.right.val);
      sb.append('R');
      backTrace(root.right, destValue, sb, visited);
      visited.remove(root.right.val);
      sb.deleteCharAt(sb.length() - 1);
    }
    
    //父节点
    if(fatherMap.containsKey(root.val)) {
      TreeNode father = fatherMap.get(root.val);
      if(!visited.contains(father.val)) {
        visited.add(father.val);
        sb.append('U');
        backTrace(father, destValue, sb, visited);
        visited.remove(father.val);
        sb.deleteCharAt(sb.length() - 1);
      }
    }
  }
  
  private void dfs(TreeNode root, int startValue) {
    if(root == null) return;
    if(root.val == startValue) startNode = root;
    if(root.left != null) {
      fatherMap.put(root.left.val, root);
      dfs(root.left, startValue);
    }
    
    if(root.right != null) {
      fatherMap.put(root.right.val, root);
      dfs(root.right, startValue);
    }
  }
}
```

------

### 题目四、[5932. 合法重新排列数对](https://leetcode-cn.com/problems/valid-arrangement-of-pairs/)【困难】

#### 题目描述

给你一个下标从 **0** 开始的二维整数数组 `pairs` ，其中 `pairs[i] = [starti, endi]` 。如果 `pairs` 的一个重新排列，满足对每一个下标 `i` （ `1 <= i < pairs.length` ）都有 `endi-1 == starti` ，那么我们就认为这个重新排列是 `pairs` 的一个 **合法重新排列** 。

请你返回 **任意一个** `pairs` 的合法重新排列。

**注意：**数据保证至少存在一个 `pairs` 的合法重新排列。

 

**示例 1：**

```
输入：pairs = [[5,1],[4,5],[11,9],[9,4]]
输出：[[11,9],[9,4],[4,5],[5,1]]
解释：
输出的是一个合法重新排列，因为每一个 endi-1 都等于 starti 。
end0 = 9 == 9 = start1 
end1 = 4 == 4 = start2
end2 = 5 == 5 = start3
```

**示例 2：**

```
输入：pairs = [[1,3],[3,2],[2,1]]
输出：[[1,3],[3,2],[2,1]]
解释：
输出的是一个合法重新排列，因为每一个 endi-1 都等于 starti 。
end0 = 3 == 3 = start1
end1 = 2 == 2 = start2
重新排列后的数组 [[2,1],[1,3],[3,2]] 和 [[3,2],[2,1],[1,3]] 都是合法的。
```

**示例 3：**

```
输入：pairs = [[1,2],[1,3],[2,1]]
输出：[[1,2],[2,1],[1,3]]
解释：
输出的是一个合法重新排列，因为每一个 endi-1 都等于 starti 。
end0 = 2 == 2 = start1
end1 = 1 == 1 = start2
```

 

**提示：**

- `1 <= pairs.length <= 10^5`
- `pairs[i].length == 2`
- `0 <= starti, endi <= 10^9`
- `starti != endi`
- `pairs` 中不存在一模一样的数对。
- 至少 **存在** 一个合法的 `pairs` 重新排列。



#### 分析

本题是欧拉通路问题，也称为一笔画问题。

欧拉通路是由哥尼斯堡七桥问题演化而来的，如下图所示，流经哥尼斯堡的普雷格尔河中有两个岛，两个岛与两岸共4处陆地通过7座杨 彼此相联。7桥问题就是如何能从任一处陆地出发，经过且经过每个桥一次后回到原出发点。

![图1](https://bkimg.cdn.bcebos.com/pic/e7cd7b899e510fb30f249656207adf95d143ac4ba692?x-bce-process=image/resize,m_lfit,w_440,limit_1/format,f_auto)

上图中的七座桥每座桥有且仅能通过一次，也称为一笔画问题，一笔能够画完所有的路线。



【定义1】欧拉通路：通过图中所有边恰好一次且行遍所有顶点的通路称为欧拉通路。

【定义2】欧拉回路：通过图中所有边恰好一次且行遍所有顶点的回路称为欧拉回路。

【定义3】欧拉图：具有欧拉回路的无向图或有向图称为欧拉图。

【定义4】半欧拉图：具有欧拉通路但不具有欧拉回路的无向图或有向图称为半欧拉图。



【性质1】对于有向图 ， 是欧拉图当且仅当 的所有顶点属于同一个强连通分量且每个顶点的入度和出度相同。

【性质2】对于有向图的欧拉图，最多只有一个顶点的出度与入度差为 1，并且该节点为起始节点；最多只有一个顶点的入度与出度差为 1，并且该节点是最终节点。所有其他顶点的入度和出度相同。



本题是有向图，由于本题肯定有解，那么本题要么是欧拉图要么是半欧拉图，我们可以通过计算入度与出度的差来决定哪个是图的起点，然后通过DFS来确定最终的路径。



#### 代码

```java
class Solution {
    Map<Integer, List<Integer>> graph = new HashMap<>();
    List<int[]> result = new ArrayList<>();

    public int[][] validArrangement(int[][] pairs) {
        Map<Integer, Integer> map = new HashMap<>();

        for(int[] pair : pairs) {
            //入度加一
            map.put(pair[1], map.getOrDefault(pair[1], 0) + 1);
            //出度减一
            map.put(pair[0], map.getOrDefault(pair[0], 0) - 1);

            //构建图
            List<Integer> list = graph.getOrDefault(pair[0], new ArrayList<>());
            list.add(pair[1]);
            graph.put(pair[0], list);
        }

        //随便选择一个点作为起点
        int from = pairs[0][0];
        for(Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if(entry.getValue() == -1) from = entry.getKey();
        }

        dfs(from);

        //构造返回结果
        int[][] ans = new int[pairs.length][2];
        for(int i=0;i<result.size();i++) {
            ans[pairs.length - 1 - i] = result.get(i);
        }

        return ans;
    }

    private void dfs(int from) {
        List<Integer> list = graph.get(from);
        while(list!= null && list.size() > 0) {
            int next = list.get(0);
            list.remove(0);
            dfs(next);
            result.add(new int[]{from, next});
        }
    }
}
```

