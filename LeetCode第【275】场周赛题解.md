###### **本文主要解析LeetCode在2022年1月9日10：30组织的第【275】场周赛题目，[竞赛链接](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/contest/weekly-contest-275)。**

###### **有兴趣的同学可以关注一下我的LeetCode[个人账号](https://link.zhihu.com/?target=https%3A//leetcode-cn.com/u/chen-xiao-bin-5/)。**

------

### 题目一、[5976. 检查是否每一行每一列都包含全部整数](https://leetcode-cn.com/problems/check-if-every-row-and-column-contains-all-numbers/)【简单】

对一个大小为 `n x n` 的矩阵而言，如果其每一行和每一列都包含从 `1` 到 `n` 的 **全部** 整数（含 `1` 和 `n`），则认为该矩阵是一个 **有效** 矩阵。

给你一个大小为 `n x n` 的整数矩阵 `matrix` ，请你判断矩阵是否为一个有效矩阵：如果是，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/12/21/example1drawio.png)

```
输入：matrix = [[1,2,3],[3,1,2],[2,3,1]]
输出：true
解释：在此例中，n = 3 ，每一行和每一列都包含数字 1、2、3 。
因此，返回 true 。
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/12/21/example2drawio.png)

```
输入：matrix = [[1,1,1],[1,2,3],[1,2,3]]
输出：false
解释：在此例中，n = 3 ，但第一行和第一列不包含数字 2 和 3 。
因此，返回 false 。
```

 

**提示：**

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 100`
- `1 <= matrix[i][j] <= n`



#### 分析

本题的数据量比较小，直接模拟即可。

由于本题的数据都是在1和n之间，所以对每一行/每一列判断是使用集合即可，将所有元素加到集合当中，如果遍历完之后集合元素的个数小于n说明元素有重复，反之则不重复。

#### 代码

```python
class Solution:
    def checkValid(self, matrix: List[List[int]]) -> bool:
        n = len(matrix)
        for i in range(0, n):
            val_set = set()
            for j in range(0, n):
                val_set.add(matrix[i][j])
            if len(val_set) < n:
                return False;
        for i in range(0, n):
            val_set = set()
            for j in range(0, n):
                val_set.add(matrix[j][i])
            if len(val_set) < n:
                return False;
        return True
```

------

### 题目二、[5977. 最少交换次数来组合所有的 1 II](https://leetcode-cn.com/problems/minimum-swaps-to-group-all-1s-together-ii/)【中等】

**交换** 定义为选中一个数组中的两个 **互不相同** 的位置并交换二者的值。

**环形** 数组是一个数组，可以认为 **第一个** 元素和 **最后一个** 元素 **相邻** 。

给你一个 **二进制环形** 数组 `nums` ，返回在 **任意位置** 将数组中的所有 `1` 聚集在一起需要的最少交换次数。

 

**示例 1：**

```
输入：nums = [0,1,0,1,1,0,0]
输出：1
解释：这里列出一些能够将所有 1 聚集在一起的方案：
[0,0,1,1,1,0,0] 交换 1 次。
[0,1,1,1,0,0,0] 交换 1 次。
[1,1,0,0,0,0,1] 交换 2 次（利用数组的环形特性）。
无法在交换 0 次的情况下将数组中的所有 1 聚集在一起。
因此，需要的最少交换次数为 1 。
```

**示例 2：**

```
输入：nums = [0,1,1,1,0,0,1,1,0]
输出：2
解释：这里列出一些能够将所有 1 聚集在一起的方案：
[1,1,1,0,0,0,0,1,1] 交换 2 次（利用数组的环形特性）。
[1,1,1,1,1,0,0,0,0] 交换 2 次。
无法在交换 0 次或 1 次的情况下将数组中的所有 1 聚集在一起。
因此，需要的最少交换次数为 2 。
```

**示例 3：**

```
输入：nums = [1,1,0,0,1]
输出：0
解释：得益于数组的环形特性，所有的 1 已经聚集在一起。
因此，需要的最少交换次数为 0 。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `nums[i]` 为 `0` 或者 `1`



#### 分析

从题意可知交换完之后最终的结果是一段连续的1，所以可以使用滑动窗口解决：先统计出数组中1的个数，以此作为滑动窗口的长度，然后统计每个滑动窗口中0的个数，即需要交换的次数。

本题需要注意的是该数组是一个环形数组，所以right应该是n + 窗口长度，或者可以使用left作为判断循环结束的条件，即left < n,由于right会大于n所以在数组取下标为right值时需要特殊处理一下，使用right % n



#### 代码

```java
class Solution {
    public int minSwaps(int[] nums) {
        int oneCount = 0;
        for(int num : nums) {
            if(num == 1) oneCount++;
        }
        
        int left = 0,right = 0;
        int n = nums.length;
        int result = oneCount;
        int count = 0;
        while(left < n) {
            if(nums[right % n] == 0) count++;
            while(right - left + 1> oneCount) {
                if(nums[left] == 0) count--;
                left++;
            }
            if(right - left + 1 == oneCount) {
                result = Math.min(result, count);
            }
            right++;
        }
        
        return result;
    }
}
```

------

### 题目三、[5978. 统计追加字母可以获得的单词数](https://leetcode-cn.com/problems/count-words-obtained-after-adding-a-letter/)【中等】

给你两个下标从 **0** 开始的字符串数组 `startWords` 和 `targetWords` 。每个字符串都仅由 **小写英文字母** 组成。

对于 `targetWords` 中的每个字符串，检查是否能够从 `startWords` 中选出一个字符串，执行一次 **转换操作** ，得到的结果与当前 `targetWords` 字符串相等。

**转换操作** 如下面两步所述：

1. **追加**任何**不存在**于当前字符串的任一小写字母到当前字符串的末尾。
   - 例如，如果字符串为 `"abc"` ，那么字母 `'d'`、`'e'` 或 `'y'` 都可以加到该字符串末尾，但 `'a'` 就不行。如果追加的是 `'d'` ，那么结果字符串为 `"abcd"` 。
2. **重排**新字符串中的字母，可以按**任意**顺序重新排布字母。
   - 例如，`"abcd"` 可以重排为 `"acbd"`、`"bacd"`、`"cbda"`，以此类推。注意，它也可以重排为 `"abcd"` 自身。

找出 `targetWords` 中有多少字符串能够由 `startWords` 中的 **任一** 字符串执行上述转换操作获得。返回 `targetWords` 中这类 **字符串的数目** 。

**注意：**你仅能验证 `targetWords` 中的字符串是否可以由 `startWords` 中的某个字符串经执行操作获得。`startWords` 中的字符串在这一过程中 **不** 发生实际变更。

 

**示例 1：**

```
输入：startWords = ["ant","act","tack"], targetWords = ["tack","act","acti"]
输出：2
解释：
- 为了形成 targetWords[0] = "tack" ，可以选用 startWords[1] = "act" ，追加字母 'k' ，并重排 "actk" 为 "tack" 。
- startWords 中不存在可以用于获得 targetWords[1] = "act" 的字符串。
  注意 "act" 确实存在于 startWords ，但是 必须 在重排前给这个字符串追加一个字母。
- 为了形成 targetWords[2] = "acti" ，可以选用 startWords[1] = "act" ，追加字母 'i' ，并重排 "acti" 为 "acti" 自身。
```

**示例 2：**

```
输入：startWords = ["ab","a"], targetWords = ["abc","abcd"]
输出：1
解释：
- 为了形成 targetWords[0] = "abc" ，可以选用 startWords[0] = "ab" ，追加字母 'c' ，并重排为 "abc" 。
- startWords 中不存在可以用于获得 targetWords[1] = "abcd" 的字符串。
```

 

**提示：**

- `1 <= startWords.length, targetWords.length <= 5 * 10^4`
- `1 <= startWords[i].length, targetWords[j].length <= 26`
- `startWords` 和 `targetWords` 中的每个字符串都仅由小写英文字母组成
- 在 `startWords` 或 `targetWords` 的任一字符串中，每个字母至多出现一次



#### 分析

本题可以通过穷举startWords数组可能通过转换操作生成的所有单词，统计出哪些单词在targetWords中。

比较的时候我们可以通过对所有的单词按照字母排序，如果排序后的字符串相等，那么这两个字符串可以通过转换操作中的重排操作成同一个字符串。比如startWords中有字符串“ac”，targetWords中有“bca”和“bac”，startWords中的字符串可以添加字符'b'，然后按照字符串排序成"abc",将targetWords中的"bca"和"bac"都通过字符串排序生成"abc"，即"ac"可以通过转换操作生成"bca"和"bac"。

解题步骤如下：

1.将targetWords中的所有字符串按照字符顺序排序存放在Map中，key为排序后的字符串，value为该字符串出现的次数。

2.遍历startWords中的每个字符串，在字符串末尾加上一个在字符，并且按照字符串进行排序。如果排序后的字符串在Map中存在，则在结果加上该字符串在map中的value，即出现的次数。



#### 代码

```java
class Solution {
    public int wordCount(String[] startWords, String[] targetWords) {
        //对targetWords进行排序，并记录频次
        Map<String, Integer> targetMap = new HashMap<>();
        for(String target : targetWords) {
            String s = sortStr(target);
            targetMap.put(s, targetMap.getOrDefault(s, 0) + 1);
        }
        
        int result = 0;
        for(String start : startWords) {
          //遍历26个字母，在start的后面加上每一个字母
            for(int i=0;i<26;i++) {
                char c = (char)('a' + i);
                String str = sortStr(start + c);
                //如果targetMap中存在，则加上出现的频次
                if(targetMap.containsKey(str)) {
                    result += targetMap.get(str);
                  	//需要删除已经统计过的单词，避免重复统计
                    targetMap.remove(str);
                }
            }
        }
        
        return result;
    }
    
    
    private static String sortStr(String str) {
		char[] charArray = str.toCharArray();
		StringBuilder result = new StringBuilder();
		// 对数组排序
		Arrays.sort(charArray);
        for(char c : charArray) {
            result.append(c);
        }
        
        return result.toString();
    }
}
```

------

### 题目四、[5979. 全部开花的最早一天](https://leetcode-cn.com/problems/earliest-possible-day-of-full-bloom/)【困难】

你有 `n` 枚花的种子。每枚种子必须先种下，才能开始生长、开花。播种需要时间，种子的生长也是如此。给你两个下标从 **0** 开始的整数数组 `plantTime` 和 `growTime` ，每个数组的长度都是 `n` ：

- `plantTime[i]` 是 **播种** 第 `i` 枚种子所需的 **完整天数** 。每天，你只能为播种某一枚种子而劳作。**无须** 连续几天都在种同一枚种子，但是种子播种必须在你工作的天数达到 `plantTime[i]` 之后才算完成。
- `growTime[i]` 是第 `i` 枚种子完全种下后生长所需的 **完整天数** 。在它生长的最后一天 **之后** ，将会开花并且永远 **绽放** 。

从第 `0` 开始，你可以按 **任意** 顺序播种种子。

返回所有种子都开花的 **最早** 一天是第几天。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/12/21/1.png)

```
输入：plantTime = [1,4,3], growTime = [2,3,1]
输出：9
解释：灰色的花盆表示播种的日子，彩色的花盆表示生长的日子，花朵表示开花的日子。
一种最优方案是：
第 0 天，播种第 0 枚种子，种子生长 2 整天。并在第 3 天开花。
第 1、2、3、4 天，播种第 1 枚种子。种子生长 3 整天，并在第 8 天开花。
第 5、6、7 天，播种第 2 枚种子。种子生长 1 整天，并在第 9 天开花。
因此，在第 9 天，所有种子都开花。 
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/12/21/2.png)

```
输入：plantTime = [1,2,3,2], growTime = [2,1,2,1]
输出：9
解释：灰色的花盆表示播种的日子，彩色的花盆表示生长的日子，花朵表示开花的日子。 
一种最优方案是：
第 1 天，播种第 0 枚种子，种子生长 2 整天。并在第 4 天开花。
第 0、3 天，播种第 1 枚种子。种子生长 1 整天，并在第 5 天开花。
第 2、4、5 天，播种第 2 枚种子。种子生长 2 整天，并在第 8 天开花。
第 6、7 天，播种第 3 枚种子。种子生长 1 整天，并在第 9 天开花。
因此，在第 9 天，所有种子都开花。 
```

**示例 3：**

```
输入：plantTime = [1], growTime = [1]
输出：2
解释：第 0 天，播种第 0 枚种子。种子需要生长 1 整天，然后在第 2 天开花。
因此，在第 2 天，所有种子都开花。
```

 

**提示：**

- `n == plantTime.length == growTime.length`
- `1 <= n <= 105`
- `1 <= plantTime[i], growTime[i] <= 10^4`



#### 分析

无论哪个花先种，种植时间的总和都是一样的，即plantTime数组的总和是一致的，最终决定全部开花的时间是全部花种植完成之后的成长时间，如果全部种植完成之后等到全部开花需要成长的时间越短，那么全部开花最早。所以让成长时间越长的花越早种植越好。



#### 代码

```java
class Solution {
 public int earliestFullBloom(int[] plantTime, int[] growTime) {
        int result = 0;
        int n = plantTime.length;
        PriorityQueue<Node> queue = new PriorityQueue<>((p1, p2) -> (p2.growTime - p1.growTime));
        for(int i=0;i<n;i++) {
            Node node = new Node(plantTime[i], growTime[i]);
            queue.offer(node);
        }
        
        int t = 0;
        int max = 0;
        while(!queue.isEmpty()) {
            Node node = queue.poll();
            max = Math.max(max, t + node.plantT + node.growTime);
            t += node.plantT;
        }
        
        return max;
    }

    class Node {
        int plantT;
        int growTime;

        public Node(int plantT, int growTime) {
            this.plantT = plantT;
            this.growTime = growTime;
        }
    }
}
```

