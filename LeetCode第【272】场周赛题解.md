###### 本文主要解析LeetCode在2021年12月19日10：30组织的第【272】场周赛题目，[竞赛链接](https://leetcode-cn.com/contest/weekly-contest-272)。

###### 有兴趣的同学可以关注一下我的LeetCode[个人账号](https://leetcode-cn.com/u/chen-xiao-bin-5/)。

###### 周赛群人数过多，只能通过邀请进群，有兴趣一起打周赛的同学可以添加我的微信号：cbbdwx，拉你进群

---
### 题目一、[5956. 找出数组中的第一个回文字符串](https://leetcode-cn.com/problems/find-first-palindromic-string-in-the-array/)

#### 题目描述

给你一个字符串数组 `words` ，找出并返回数组中的 **第一个回文字符串** 。如果不存在满足要求的字符串，返回一个 **空字符串** `""` 。

**回文字符串** 的定义为：如果一个字符串正着读和反着读一样，那么该字符串就是一个 **回文字符串** 。

 

**示例 1：**

```
输入：words = ["abc","car","ada","racecar","cool"]
输出："ada"
解释：第一个回文字符串是 "ada" 。
注意，"racecar" 也是回文字符串，但它不是第一个。
```

**示例 2：**

```
输入：words = ["notapalindrome","racecar"]
输出："racecar"
解释：第一个也是唯一一个回文字符串是 "racecar" 。
```

**示例 3：**

```
输入：words = ["def","ghi"]
输出：""
解释：不存在回文字符串，所以返回一个空字符串。
```

 

**提示：**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i]` 仅由小写英文字母组成



#### 分析

回文字符串



#### 代码

```java
class Solution {
    public String firstPalindrome(String[] words) {
        for(String word : words) {
            if(palindromeCheck(word)) return word;
        }
        
        return "";
    }
    
    private boolean palindromeCheck(String str) {
        int l=0,r=str.length() - 1;
        while(l < r) {
            if(str.charAt(l) != str.charAt(r)) {
                return false;
            }
            l++;
            r--;
        }
        
        return true;
    }
}
```

---

### 题目二、[5957. 向字符串添加空格](https://leetcode-cn.com/problems/adding-spaces-to-a-string/)

#### 题目描述

给你一个下标从 **0** 开始的字符串 `s` ，以及一个下标从 **0** 开始的整数数组 `spaces` 。

数组 `spaces` 描述原字符串中需要添加空格的下标。每个空格都应该插入到给定索引处的字符值 **之前** 。

- 例如，`s = "EnjoyYourCoffee"` 且 `spaces = [5, 9]` ，那么我们需要在 `'Y'` 和 `'C'` 之前添加空格，这两个字符分别位于下标 `5` 和下标 `9` 。因此，最终得到 `"Enjoy ***Y***our ***C***offee"` 。

请你添加空格，并返回修改后的字符串*。*

 

**示例 1：**

```
输入：s = "LeetcodeHelpsMeLearn", spaces = [8,13,15]
输出："Leetcode Helps Me Learn"
解释：
下标 8、13 和 15 对应 "LeetcodeHelpsMeLearn" 中加粗斜体字符。
接着在这些字符前添加空格。
```

**示例 2：**

```
输入：s = "icodeinpython", spaces = [1,5,7,9]
输出："i code in py thon"
解释：
下标 1、5、7 和 9 对应 "icodeinpython" 中加粗斜体字符。
接着在这些字符前添加空格。
```

**示例 3：**

```
输入：s = "spacing", spaces = [0,1,2,3,4,5,6]
输出：" s p a c i n g"
解释：
字符串的第一个字符前可以添加空格。
```

 

**提示：**

- `1 <= s.length <= 3 * 10^5`
- `s` 仅由大小写英文字母组成
- `1 <= spaces.length <= 3 * 10^5`
- `0 <= spaces[i] <= s.length - 1`
- `spaces` 中的所有值 **严格递增**



#### 分析

直接模拟题意即可



#### 代码

```java
class Solution {
    public String addSpaces(String s, int[] spaces) {
        int n = s.length();
        StringBuilder sb = new StringBuilder();
        int index = 0;
        for(int i=0;i<n;i++) {
            if(index < spaces.length && i == spaces[index]) {
                sb.append(" ");
                index++;
            }
            sb.append(s.charAt(i));
        }
        
        return sb.toString();
    }
}
```

---

### 题目三、[5958. 股票平滑下跌阶段的数目](https://leetcode-cn.com/problems/number-of-smooth-descent-periods-of-a-stock/)

#### 题目描述

给你一个整数数组 `prices` ，表示一支股票的历史每日股价，其中 `prices[i]` 是这支股票第 `i` 天的价格。

一个 **平滑下降的阶段** 定义为：对于 **连续一天或者多天** ，每日股价都比 **前一日股价恰好少** `1` ，这个阶段第一天的股价没有限制。

请你返回 **平滑下降阶段** 的数目。

 

**示例 1：**

```
输入：prices = [3,2,1,4]
输出：7
解释：总共有 7 个平滑下降阶段：
[3], [2], [1], [4], [3,2], [2,1] 和 [3,2,1]
注意，仅一天按照定义也是平滑下降阶段。
```

**示例 2：**

```
输入：prices = [8,6,7,7]
输出：4
解释：总共有 4 个连续平滑下降阶段：[8], [6], [7] 和 [7]
由于 8 - 6 ≠ 1 ，所以 [8,6] 不是平滑下降阶段。
```

**示例 3：**

```
输入：prices = [1]
输出：1
解释：总共有 1 个平滑下降阶段：[1]
```

 

**提示：**

- `1 <= prices.length <= 10^5`
- `1 <= prices[i] <= 10^5`



#### 分析

本题可以分成两部分：

1.求满足题意的天数段；

2.求每个天数段组成的平滑下降阶段个数；



比如示例1：[3,2,1,4]

1.可以将示例分解成两个满足题意的连续天数：[3,2,1]和[4]

2.[3,2,1] 有[3]、[2]、[1]、[3, 2]、[2, 1], [3，2，1] 总共6个平滑下降阶段

[4] 只有1个平滑下降阶段

所以总共有7个平滑下降阶段。



一般的，如果有一个元素为n个的连续天数段，那么可分解为：

1.有1个元素的平滑下降阶段，总共有n个；

2.有2个元素的平滑下降阶段，总共有n-1；

3.有3个元素的平滑下降阶段，总共有n-2个；

...

n.有n个元素的平滑下降阶段，总共有1个

所以下降阶段的总数为 n + (n - 1) + (n - 2) + ... + 1 = (n + 1) * n / 2

即：**如果有一个元素为n个的连续天数段，那么平滑下降阶段的个数为(n + 1) * n / 2**

示例中有3个和1个的连续天数段，所以平滑下降阶段个数为:

(3 + 1) * 3 / 2 = 6

(1 + 1) * 1 / 2 = 1

6 + 1 = 7



#### 代码

```java
class Solution {
  public long getDescentPeriods(int[] prices) {
    int n = prices.length;
    long result = 0L;
    for(int i=0;i<n;i++) {
      //计算每一个连续天数段的元素个数
      long count = 1L;
      while(i + 1 < n && prices[i] - prices[i + 1] == 1){
        count++;
        i++;
      }            
      
      //每个连续天数段的平滑下降阶段个数
      result += ((count + 1) * count) / 2;
    }
    return result;
  }
}
```

------

### 题目四、[2111. 使数组 K 递增的最少操作次数](https://leetcode-cn.com/problems/minimum-operations-to-make-the-array-k-increasing/)【困难】

#### 题目描述

给你一个下标从 **0** 开始包含 `n` 个正整数的数组 `arr` ，和一个正整数 `k` 。

如果对于每个满足 `k <= i <= n-1` 的下标 `i` ，都有 `arr[i-k] <= arr[i]` ，那么我们称 `arr` 是 **K** **递增** 的。

- 比方说，

  ```
  arr = [4, 1, 5, 2, 6, 2]
  ```

   对于 

  ```
  k = 2
  ```

   是 K 递增的，因为：

  - `arr[0] <= arr[2] (4 <= 5)`
  - `arr[1] <= arr[3] (1 <= 2)`
  - `arr[2] <= arr[4] (5 <= 6)`
  - `arr[3] <= arr[5] (2 <= 2)`

- 但是，相同的数组 `arr` 对于 `k = 1` 不是 K 递增的（因为 `arr[0] > arr[1]`），对于 `k = 3` 也不是 K 递增的（因为 `arr[0] > arr[3]` ）。

每一次 **操作** 中，你可以选择一个下标 `i` 并将 `arr[i]` **改成任意** 正整数。

请你返回对于给定的 `k` ，使数组变成 K 递增的 **最少操作次数** 。

 

**示例 1：**

```
输入：arr = [5,4,3,2,1], k = 1
输出：4
解释：
对于 k = 1 ，数组最终必须变成非递减的。
可行的 K 递增结果数组为 [5,6,7,8,9]，[1,1,1,1,1]，[2,2,3,4,4] 。它们都需要 4 次操作。
次优解是将数组变成比方说 [6,7,8,9,10] ，因为需要 5 次操作。
显然我们无法使用少于 4 次操作将数组变成 K 递增的。
```

**示例 2：**

```
输入：arr = [4,1,5,2,6,2], k = 2
输出：0
解释：
这是题目描述中的例子。
对于每个满足 2 <= i <= 5 的下标 i ，有 arr[i-2] <= arr[i] 。
由于给定数组已经是 K 递增的，我们不需要进行任何操作。
```

**示例 3：**

```
输入：arr = [4,1,5,2,6,2], k = 3
输出：2
解释：
下标 3 和 5 是仅有的 3 <= i <= 5 且不满足 arr[i-3] <= arr[i] 的下标。
将数组变成 K 递增的方法之一是将 arr[3] 变为 4 ，且将 arr[5] 变成 5 。
数组变为 [4,1,5,4,6,5] 。
可能有其他方法将数组变为 K 递增的，但没有任何一种方法需要的操作次数小于 2 次。
```

 

**提示：**

- `1 <= arr.length <= 10^5`
- `1 <= arr[i], k <= arr.length`



#### 分析

本题分成两部分：

1.将数组分成k个子数组。

2.计算将每个数组变成非递减的操作次数。



如何计算将每个数组变成非递减的最少操作次数，可以通过计算数组的最长递增子序列，然后对不在最长递增子序列中的元素进行操作，即可得最少操作次数。

最长递增子序列可参考：[300. 最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)



#### 代码

```java
class Solution {
    public int kIncreasing(int[] arr, int k) {
        int result = 0;
        for(int i=0;i<k;i++) {
            List<Integer> list = new ArrayList<>();
            for(int j=i;j<arr.length;j+=k) {
                list.add(arr[j]);
            }
            
            result += change(list);
        }
        
        return result;
    }

    private int change(List<Integer> list) {
        int[] nums = new int[list.size()];
        for(int i=0;i<list.size();i++) {
            nums[i] = list.get(i);
        } 
        
        return list.size() - lengthOfLIS(nums);
    }
    
    public int lengthOfLIS(int[] nums) {
        int len = 1, n = nums.length;
        if (n == 0) {
            return 0;
        }
        int[] d = new int[n + 1];
        d[len] = nums[0];
        for (int i = 1; i < n; ++i) {
            if (nums[i] >= d[len]) {
                d[++len] = nums[i];
            } else {
                int l = 1, r = len, pos = 0; // 如果找不到说明所有的数都比 nums[i] 大，此时要更新 d[1]，所以这里将 pos 设为 0
                while (l <= r) {
                    int mid = (l + r) >> 1;
                    if (d[mid] <= nums[i]) {
                        pos = mid;
                        l = mid + 1;
                    } else {
                        r = mid - 1;
                    }
                }
                d[pos + 1] = nums[i];
            }
        }
        return len;
    }
}
```





