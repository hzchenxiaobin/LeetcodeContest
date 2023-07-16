###### **本文主要解析LeetCode在2023年6月24日22:30组织的第【107】场双周赛题目，**[**竞赛链接**](https://leetcode-cn.com/contest/biweekly-contest-107)**。**

###### **有兴趣的同学可以关注一下我的LeetCode**[**个人账号**](https://leetcode-cn.com/u/hzchenxiaobin/)**。**

---

### 题目一、[最大字符串配对数目](https://leetcode.cn/contest/biweekly-contest-107/problems/find-maximum-number-of-string-pairs/)【简单】

#### 题目描述

给你一个下标从 **0** 开始的数组 `words` ，数组中包含 **互不相同** 的字符串。

如果字符串 `words[i]` 与字符串 `words[j]` 满足以下条件，我们称它们可以匹配：

- 字符串 `words[i]` 等于 `words[j]` 的反转字符串。
- `0 <= i < j < words.length`

请你返回数组 `words` 中的 **最大** 匹配数目。

注意，每个字符串最多匹配一次。

 

**示例 1：**

```
输入：words = ["cd","ac","dc","ca","zz"]
输出：2
解释：在此示例中，我们可以通过以下方式匹配 2 对字符串：
- 我们将第 0 个字符串与第 2 个字符串匹配，因为 word[0] 的反转字符串是 "dc" 并且等于 words[2]。
- 我们将第 1 个字符串与第 3 个字符串匹配，因为 word[1] 的反转字符串是 "ca" 并且等于 words[3]。
可以证明最多匹配数目是 2 。
```

**示例 2：**

```
输入：words = ["ab","ba","cc"]
输出：1
解释：在此示例中，我们可以通过以下方式匹配 1 对字符串：
- 我们将第 0 个字符串与第 1 个字符串匹配，因为 words[1] 的反转字符串 "ab" 与 words[0] 相等。
可以证明最多匹配数目是 1 。
```

**示例 3：**

```
输入：words = ["aa","ab"]
输出：0
解释：这个例子中，无法匹配任何字符串。
```

 

**提示：**

- `1 <= words.length <= 50`
- `words[i].length == 2`
- `words` 包含的字符串互不相同。
- `words[i]` 只包含小写英文字母。

#### 分析

数据量比较小，逐一比较即可

#### 代码

```python
class Solution:
    def maximumNumberOfStringPairs(self, words: List[str]) -> int:
        n = len(words)
        res = 0
        for i in range(n):
            for j in range(i+1, n):
                if words[i] == words[j][::-1]:
                    res += 1
        return res
```



------

### 题目二、[构造最长的新字符串](https://leetcode.cn/contest/biweekly-contest-107/problems/construct-the-longest-new-string/)【中等】

#### 题目描述

给你三个整数 `x` ，`y` 和 `z` 。

这三个整数表示你有 `x` 个 `"AA"` 字符串，`y` 个 `"BB"` 字符串，和 `z` 个 `"AB"` 字符串。你需要选择这些字符串中的部分字符串（可以全部选择也可以一个都不选择），将它们按顺序连接得到一个新的字符串。新字符串不能包含子字符串 `"AAA"` 或者 `"BBB"` 。

请你返回新字符串的最大可能长度。

**子字符串** 是一个字符串中一段连续 **非空** 的字符序列。

 

**示例 1：**

```
输入：x = 2, y = 5, z = 1
输出：12
解释： 我们可以按顺序连接 "BB" ，"AA" ，"BB" ，"AA" ，"BB" 和 "AB" ，得到新字符串 "BBAABBAABBAB" 。
字符串长度为 12 ，无法得到一个更长的符合题目要求的字符串。
```

**示例 2：**

```
输入：x = 3, y = 2, z = 2
输出：14
解释：我们可以按顺序连接 "AB" ，"AB" ，"AA" ，"BB" ，"AA" ，"BB" 和 "AA" ，得到新字符串 "ABABAABBAABBAA" 。
字符串长度为 14 ，无法得到一个更长的符合题目要求的字符串。
```

 

**提示：**

- `1 <= x, y, z <= 50`

#### 分析

1.无论x、y、z如何分布，AB是所有都可以加在字符串上的，所以只要考虑x和y的分布

2.第一种情况：x ==  y，此时可以将字符串写成AABB这种形式，满足条件，所以可以将所有的字符串都加上。

第二种情况：x == y + 1,此时可以将字符串写成AABBAA这种形式，满足条件，所以可以将所有的字符串都加上。

第三种情况：x == y + 2,如下图所示，BB无论插在哪个位置都不满足题意，所以最终的字符串x最多比y多一个，反过来也是

![image-20230708213342945](/Users/chenbinbin/Library/Application Support/typora-user-images/image-20230708213342945.png)

所以最终可以写成：res = min(x, y) + z, 

if x != y: res += 1 

#### 代码

```Python
class Solution:
    def longestString(self, x: int, y: int, z: int) -> int:
        res = z + 2 * min(x, y)
        if x != y:
            res += 1
        return 2 * res     
```

------

### 题目三、[字符串连接删减字母](https://leetcode.cn/contest/biweekly-contest-107/problems/decremental-string-concatenation/)【中等】

#### 题目描述

给你一个下标从 **0** 开始的数组 `words` ，它包含 `n` 个字符串。

定义 **连接** 操作 `join(x, y)` 表示将字符串 `x` 和 `y` 连在一起，得到 `xy` 。如果 `x` 的最后一个字符与 `y` 的第一个字符相等，连接后两个字符中的一个会被 **删除** 。

比方说 `join("ab", "ba") = "aba"` ， `join("ab", "cde") = "abcde"` 。

你需要执行 `n - 1` 次 **连接** 操作。令 `str0 = words[0]` ，从 `i = 1` 直到 `i = n - 1` ，对于第 `i` 个操作，你可以执行以下操作之一：

- 令 `stri = join(stri - 1, words[i])`
- 令 `stri = join(words[i], stri - 1)`

你的任务是使 `strn - 1` 的长度 **最小** 。

请你返回一个整数，表示 `strn - 1` 的最小长度。

 

**示例 1：**

```
输入：words = ["aa","ab","bc"]
输出：4
解释：这个例子中，我们按以下顺序执行连接操作，得到 str2 的最小长度：
str0 = "aa"
str1 = join(str0, "ab") = "aab"
str2 = join(str1, "bc") = "aabc" 
str2 的最小长度为 4 。
```

**示例 2：**

```
输入：words = ["ab","b"]
输出：2
解释：这个例子中，str0 = "ab"，可以得到两个不同的 str1：
join(str0, "b") = "ab" 或者 join("b", str0) = "bab" 。
第一个字符串 "ab" 的长度最短，所以答案为 2 。
```

**示例 3：**

```
输入：words = ["aaa","c","aba"]
输出：6
解释：这个例子中，我们按以下顺序执行连接操作，得到 str2 的最小长度：
str0 = "aaa"
str1 = join(str0, "c") = "aaac"
str2 = join("aba", str1) = "abaaac"
str2 的最小长度为 6 。
```

 

**提示：**

- `1 <= words.length <= 1000`
- `1 <= words[i].length <= 50`
- `words[i]` 中只包含小写英文字母。

#### 分析

动态规划

我们只关注字符串的第一个字符和最后一个字符，所以可以创建数组dp(i, j, k)，i表示数组中的第i个字符串，j表示字符串的第一个字符，k表示字符串的最后一个字符。



递推方式有两种：1.放在前面，2.放在后面

1.放在前面(放在前面的时候，字符串的第一个字符会发生修改，所以第二维的索引要进行修改)

假设 x = word[0], y = word[-1]
$$
dp[i][x][k] = min\{
{dp[i-1][j][k] + len(word) \quad当word的末尾字母不等于字符串的首字母，也就是y != j 
\atop dp[i-1][j][k] + len(word) - 1 \quad当word的末尾字母等于字符串的首字母，也就是y == j}
$$


2.放在后面(放在后面的时候，字符串的第一个字符会发生修改，所以第二维的索引要进行修改)
$$
dp[i][j][y] = min\{{dp[i-1][j][k] + len(word) \quad当word的首字母不等于字符串的尾字母，也就是x != k 
\atop dp[i-1][j][k] + len(word) - 1 \quad当word的首字母不等于字符串的尾字母，也就是x == k}
$$


#### 代码

```python
class Solution:
    def minimizeConcatenatedLength(self, words: List[str]) -> int:
        n = len(words)
        dp = [[[inf for i in range(26)] for j in range(26)] for k in range(n)]
        dp[0][ord(words[0][0]) - ord('a')][ord(words[0][-1]) - ord('a')] = len(words[0])    
        
        for i in range(1, n):
            word = words[i]            
            for j in range(26):
                for k in range(26):
                    if dp[i-1][j][k] == inf:
                        continue
                    x, y = ord(word[0])  - ord('a'), ord(word[-1])  - ord('a')
                    # 加在前面
                    dp[i][x][k] = min(dp[i][x][k], dp[i-1][j][k] + len(word) - 1 if y == j else dp[i-1][j][k] + len(word))
                    # 加在后面
                    dp[i][j][y] = min(dp[i][j][y], dp[i-1][j][k] + len(word) - 1 if x == k else dp[i-1][j][k] + len(word))
    
        res = inf
        for j in range(26):
            for k in range(26):
                res = min(res, dp[n-1][j][k])
        return res
```

------

### 题目四、[统计没有收到请求的服务器数目](https://leetcode.cn/contest/biweekly-contest-107/problems/count-zero-request-servers/)【中等】

#### 题目描述

给你一个整数 `n` ，表示服务器的总数目，再给你一个下标从 **0** 开始的 **二维** 整数数组 `logs` ，其中 `logs[i] = [server_id, time]` 表示 id 为 `server_id` 的服务器在 `time` 时收到了一个请求。

同时给你一个整数 `x` 和一个下标从 **0** 开始的整数数组 `queries` 。

请你返回一个长度等于 `queries.length` 的数组 `arr` ，其中 `arr[i]` 表示在时间区间 `[queries[i] - x, queries[i]]` 内没有收到请求的服务器数目。

注意时间区间是个闭区间。

 

**示例 1：**

```
输入：n = 3, logs = [[1,3],[2,6],[1,5]], x = 5, queries = [10,11]
输出：[1,2]
解释：
对于 queries[0]：id 为 1 和 2 的服务器在区间 [5, 10] 内收到了请求，所以只有服务器 3 没有收到请求。
对于 queries[1]：id 为 2 的服务器在区间 [6,11] 内收到了请求，所以 id 为 1 和 3 的服务器在这个时间段内没有收到请求。
```

**示例 2：**

```
输入：n = 3, logs = [[2,4],[2,1],[1,2],[3,1]], x = 2, queries = [3,4]
输出：[0,1]
解释：
对于 queries[0]：区间 [1, 3] 内所有服务器都收到了请求。
对于 queries[1]：只有 id 为 3 的服务器在区间 [2,4] 内没有收到请求。
```

 

**提示：**

- `1 <= n <= 10^5`
- `1 <= logs.length <= 10^5`
- `1 <= queries.length <= 10^5`
- `logs[i].length == 2`
- `1 <= logs[i][0] <= n`
- `1 <= logs[i][1] <= 10^6`
- `1 <= x <= 10^5`
- `x < queries[i] <= 10^6`

#### 分析

把sorted_logs和sorted_queries排序后，滑动窗口即可，窗口的长度为x

#### 代码

```python
class Solution:
    def countServers(self, n: int, logs: List[List[int]], x: int, queries: List[int]) -> List[int]:
        map = dict()
        query_map = dict()
        sorted_logs = sorted(logs, key=lambda x: x[1])
        sorted_queries = sorted(queries)
        left,right = 0,0
        for query in sorted_queries:
            while right < len(sorted_logs) and sorted_logs[right][1] <= query:
                server_id,time = sorted_logs[right][0], sorted_logs[right][1]
                map[server_id] = map.get(server_id, 0) + 1
                right += 1
            
            while left <= right and left < len(sorted_logs) and sorted_logs[left][1] < query - x:
                s_id = sorted_logs[left][0]
                map[s_id] -= 1
                if map[s_id] == 0:
                    del map[s_id]
                left += 1
            query_map[query] = n - len(map)
        
        res = [0 for i in range(len(queries))]
        for i in range(len(queries)):
            query = queries[i]
            if query in query_map:
                res[i] = query_map[query]
        
        return res
```

