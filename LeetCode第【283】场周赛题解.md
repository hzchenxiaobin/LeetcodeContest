### 题目一、[6016. Excel 表中某个范围内的单元格](https://leetcode-cn.com/problems/cells-in-a-range-on-an-excel-sheet/)【简单】

#### 题目描述

Excel 表中的一个单元格 `(r, c)` 会以字符串 `"<col><row>"` 的形式进行表示，其中：

- <col> 即单元格的列号 c 。用英文字母表中的 字母 标识。
  例如，第 1 列用 'A' 表示，第 2 列用 'B' 表示，第 3 列用 'C' 表示，以此类推。
- `<row>` 即单元格的行号 `r` 。第 `r` 行就用 **整数** `r` 标识。

给你一个格式为 `"<col1><row1>:<col2><row2>"` 的字符串 `s` ，其中 `<col1>` 表示 `c1` 列，`<row1>` 表示 `r1` 行，`<col2>` 表示 `c2` 列，`<row2>` 表示 `r2` 行，并满足 `r1 <= r2` 且 `c1 <= c2` 。

找出所有满足 `r1 <= x <= r2` 且 `c1 <= y <= c2` 的单元格，并以列表形式返回。单元格应该按前面描述的格式用 **字符串** 表示，并以 **非递减** 顺序排列（先按列排，再按行排）。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2022/02/08/ex1drawio.png)

```
输入：s = "K1:L2"
输出：["K1","K2","L1","L2"]
解释：
上图显示了列表中应该出现的单元格。
红色箭头指示单元格的出现顺序。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2022/02/09/exam2drawio.png)

```
输入：s = "A1:F1"
输出：["A1","B1","C1","D1","E1","F1"]
解释：
上图显示了列表中应该出现的单元格。 
红色箭头指示单元格的出现顺序。
```

 

**提示：**

- `s.length == 5`
- `'A' <= s[0] <= s[3] <= 'Z'`
- `'1' <= s[1] <= s[4] <= '9'`
- `s` 由大写英文字母、数字、和 `':'` 组成



#### 分析

模拟即可，找到开始的字母、数字和结束的字母、数字，两层循环即可。



#### 代码

```java
class Solution {
    public List<String> cellsInRange(String s) {
        String[] arr = s.split(":");
        
        char startC = arr[0].charAt(0), endC = arr[1].charAt(0);
        int startN = arr[0].charAt(1) - '0', endN = arr[1].charAt(1) - '0';
        
        List<String> res = new ArrayList<>();
        for(char c = startC; c <= endC; c = (char)((int)c + 1)) {
            for(int p = startN;p<= endN;p++) {
                res.add(c + "" + p);
            }
        }
        
        return res;
    }
}
```

------

### 题目二、[6017. 向数组中追加 K 个整数](https://leetcode-cn.com/problems/append-k-integers-with-minimal-sum/)【中等】

#### 题目描述

给你一个整数数组 `nums` 和一个整数 `k` 。请你向 `nums` 中追加 `k` 个 **未** 出现在 `nums` 中的、**互不相同** 的 **正** 整数，并使结果数组的元素和 **最小** 。

返回追加到 `nums` 中的 `k` 个整数之和。

 

**示例 1：**

```
输入：nums = [1,4,25,10,25], k = 2
输出：5
解释：在该解法中，向数组中追加的两个互不相同且未出现的正整数是 2 和 3 。
nums 最终元素和为 1 + 4 + 25 + 10 + 25 + 2 + 3 = 70 ，这是所有情况中的最小值。
所以追加到数组中的两个整数之和是 2 + 3 = 5 ，所以返回 5 。
```

**示例 2：**

```
输入：nums = [5,6], k = 6
输出：25
解释：在该解法中，向数组中追加的两个互不相同且未出现的正整数是 1 、2 、3 、4 、7 和 8 。
nums 最终元素和为 5 + 6 + 1 + 2 + 3 + 4 + 7 + 8 = 36 ，这是所有情况中的最小值。
所以追加到数组中的两个整数之和是 1 + 2 + 3 + 4 + 7 + 8 = 25 ，所以返回 25 。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i], k <= 10^9`



#### 分析

需要追加k个数并使得数组之和最小，暴力的方法是从1开始遍历，如果该数字不存在于原数组中，则加入。

```java
class Solution {
    public long minimalKSum(int[] nums, int k) {
        Set<Integer> set = new HashSet<>();
        for(int num : nums) set.add(num);
        
        int num = 1;
        long result = 0L;
        while(k > 0) {
            // 不包含则加入
            if(!set.contains(num)) {
                k--;
                result += num;
            }
            num++;
        }
        
        return result;
    }
}
```

因为k取值范围是10^9，所以上述解法会超时。



从上面解法中我们可以看出来，加入k个数后最终的结果是：

1.前半段是1~p的等差数列，即[1，2，3，4，...， p]

2.后半段是原数组的值，这部分可能有可能没有。



算法：

找到p值，求出等差数列的值减去原数组下标在p之前的数的和。

```java
for(int i=0;i<nums.length;i++) {
  if(nums[i] - (i + 1) >= k) {
    return (1 + k + i) * (k + i) / 2 - sum;
  }
  
  sum += nums[i];
}
```



存在两种情况：

1.原数组中的最大值大于p，那么遍历原数组肯定能找到答案。

2.原数组中的最大值小于p，那么遍历原数组无法找到答案，加上k个值，那么最终的数组的最大值不会超过

（max + k + 1），max为原数组中的最大值。所以我们可以在原数组中加入（max + k + 1），这样子就不需要处理边界条件。



数组中可能存在重复的值，重复的值需要去掉。



#### 代码

```java
class Solution {
    public long minimalKSum(int[] nums, int k) {
        long sum = 0L;
        List<Integer> list = new ArrayList<>();
        for(int num : nums) list.add(num);
        
        // 去重和排序
        list = list.stream()
                .distinct()
                .sorted()
                .collect(Collectors.toList());
        
        // 加入边界值
        list.add(list.get(list.size() - 1) + k + 1);
        
        for(int i=0;i<list.size();i++) {
            if(list.get(i) - (i + 1) >= k) {
                return (long)(1 + k + i) * (long)(k + i) / 2L - sum;
            }
            sum += list.get(i);
        }

        return 0L;
    }
}
```

------

### 题目三、[6018. 根据描述创建二叉树](https://leetcode-cn.com/problems/create-binary-tree-from-descriptions/)【中等】

#### 题目描述

给你一个二维整数数组 `descriptions` ，其中 `descriptions[i] = [parenti, childi, isLefti]` 表示 `parenti` 是 `childi` 在 **二叉树** 中的 **父节点**，二叉树中各节点的值 **互不相同** 。此外：

- 如果 `isLefti == 1` ，那么 `childi` 就是 `parenti` 的左子节点。
- 如果 `isLefti == 0` ，那么 `childi` 就是 `parenti` 的右子节点。

请你根据 `descriptions` 的描述来构造二叉树并返回其 **根节点** 。

测试用例会保证可以构造出 **有效** 的二叉树。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2022/02/09/example1drawio.png)

```
输入：descriptions = [[20,15,1],[20,17,0],[50,20,1],[50,80,0],[80,19,1]]
输出：[50,20,80,15,17,19]
解释：根节点是值为 50 的节点，因为它没有父节点。
结果二叉树如上图所示。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2022/02/09/example2drawio.png)

```
输入：descriptions = [[1,2,1],[2,3,0],[3,4,1]]
输出：[1,2,null,null,3,4]
解释：根节点是值为 1 的节点，因为它没有父节点。 
结果二叉树如上图所示。 
```

 

**提示：**

- `1 <= descriptions.length <= 10^4`
- `descriptions[i].length == 3`
- `1 <= parenti, childi <= 10^5`
- `0 <= isLefti <= 1`
- `descriptions` 所描述的二叉树是一棵有效二叉树

#### 分析

直接模拟即可，构建出每个TreeNode，最后需要找到根节点，根节点是入度为0的点，我们在构建树的过程中记录下每个子节点的值，所有节点中不在这些子节点的就是根节点。



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
    public TreeNode createBinaryTree(int[][] descriptions) {
        Map<Integer, TreeNode> map = new HashMap<>();
      
      	// 记录所有子节点
        Set<Integer> set = new HashSet<>();
        for(int[] des : descriptions) {
            int f = des[0], c = des[1], l = des[2];
            TreeNode node = map.getOrDefault(f, new TreeNode(f));
            TreeNode child = map.getOrDefault(c, new TreeNode(c));
            if(l == 1) {
                node.left = child;
            } else {
                node.right = child;
            }
            
            map.put(f, node);
            map.put(c, child);
            set.add(c);
        }
        
      	// 不在子节点中的就是根节点
        for(Map.Entry<Integer, TreeNode> entry : map.entrySet()) {
            if(!set.contains(entry.getKey())) {
               return entry.getValue(); 
            }
        }
        
        return null;
    }
}
```

------

### 题目四、[6019. 替换数组中的非互质数](https://leetcode-cn.com/problems/replace-non-coprime-numbers-in-array/)【困难】

#### 题目描述

给你一个整数数组 `nums` 。请你对数组执行下述操作：

1. 从 `nums` 中找出 **任意** 两个 **相邻** 的 **非互质** 数。
2. 如果不存在这样的数，**终止** 这一过程。
3. 否则，删除这两个数，并 **替换** 为它们的 **最小公倍数**（Least Common Multiple，LCM）。
4. 只要还能找出两个相邻的非互质数就继续 **重复** 这一过程。

返回修改后得到的 **最终** 数组。可以证明的是，以 **任意** 顺序替换相邻的非互质数都可以得到相同的结果。

生成的测试用例可以保证最终数组中的值 **小于或者等于** `108` 。

两个数字 `x` 和 `y` 满足 **非互质数** 的条件是：`GCD(x, y) > 1` ，其中 `GCD(x, y)` 是 `x` 和 `y` 的 **最大公约数** 。

 

**示例 1 ：**

```
输入：nums = [6,4,3,2,7,6,2]
输出：[12,7,6]
解释：
- (6, 4) 是一组非互质数，且 LCM(6, 4) = 12 。得到 nums = [12,3,2,7,6,2] 。
- (12, 3) 是一组非互质数，且 LCM(12, 3) = 12 。得到 nums = [12,2,7,6,2] 。
- (12, 2) 是一组非互质数，且 LCM(12, 2) = 12 。得到 nums = [12,7,6,2] 。
- (6, 2) 是一组非互质数，且 LCM(6, 2) = 6 。得到 nums = [12,7,6] 。
现在，nums 中不存在相邻的非互质数。
因此，修改后得到的最终数组是 [12,7,6] 。
注意，存在其他方法可以获得相同的最终数组。
```

**示例 2 ：**

```
输入：nums = [2,2,1,1,3,3,3]
输出：[2,1,1,3]
解释：
- (3, 3) 是一组非互质数，且 LCM(3, 3) = 3 。得到 nums = [2,2,1,1,3,3] 。
- (3, 3) 是一组非互质数，且 LCM(3, 3) = 3 。得到 nums = [2,2,1,1,3] 。
- (2, 2) 是一组非互质数，且 LCM(2, 2) = 2 。得到 nums = [2,1,1,3] 。
现在，nums 中不存在相邻的非互质数。 
因此，修改后得到的最终数组是 [2,1,1,3] 。 
注意，存在其他方法可以获得相同的最终数组。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^5`
- 生成的测试用例可以保证最终数组中的值 **小于或者等于** `10^8` 。



#### 分析

这是一道栈的题目，解题步骤：

1.引入两个栈left和right。

2.将数组中所有的值存入到right中。

3.如果left栈没有值，则将right的栈顶值推入到left中。

4.如果left栈有值，则取left栈顶和right栈顶的最大公约数，如果最大公约数为1，则将right栈顶的值推入到left，如果最大公约数的值大于1，则将两个数字的最大公倍数推入到right中。

5.循环往复直到right栈为空。



求两个数的最大公约数：[欧几里得算法(辗转相除法)](https://baike.baidu.com/item/%E6%AC%A7%E5%87%A0%E9%87%8C%E5%BE%97%E7%AE%97%E6%B3%95/1647675?fr=aladdin)

```java
int gcd(int m,int n){   
  if(n == 0){
    return m; 
  }
  int r = m%n;
  return gcd(n,r);
}
```



求两个数的最小公倍数：

```java
int lcm(int m, int n) {
  return m * n / gcd(m, n);
}
```



#### 代码

```java
class Solution {
     public List<Integer> replaceNonCoprimes(int[] nums) {
        Deque<Integer> left = new LinkedList<>();
        Deque<Integer> right = new LinkedList<>();

        for (int num : nums) right.offerLast(num);
        while (!right.isEmpty()) {
            if (left.isEmpty()) {
                left.offerLast(right.pollFirst());
                continue;
            }
            int r = right.pollFirst();
            int l = left.pollLast();
            int gcd = gcd(l,r);
            if (gcd > 1) {
                right.offerFirst(lcm(l,r));
            } else {
                left.offerLast(l);
                left.offerLast(r);
            }            
        }

        return new ArrayList<>(left);
    }
    
    int gcd(int m,int n){   
        if(n == 0){
            return m; 
        }
        int r = m%n;
        return gcd(n,r);
    }
    
    int lcm(int m, int n) {
        return (int)((long)m * (long)n / gcd(m, n));
    }
}
```

