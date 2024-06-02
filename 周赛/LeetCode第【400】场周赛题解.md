###### **本文主要解析LeetCode在2024年6月2日10:30组织的第【400】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-400)**。**

---

### 题目一、[候诊室中的最少椅子数](https://leetcode.cn/contest/weekly-contest-400/problems/minimum-number-of-chairs-in-a-waiting-room/)【简单】

#### 题目描述

给你一个字符串 `s`，模拟每秒钟的事件 `i`：

- 如果 `s[i] == 'E'`，表示有一位顾客进入候诊室并占用一把椅子。
- 如果 `s[i] == 'L'`，表示有一位顾客离开候诊室，从而释放一把椅子。

返回保证每位进入候诊室的顾客都能有椅子坐的 **最少** 椅子数，假设候诊室最初是 **空的** 。

 

**示例 1：**

**输入：**s = "EEEEEEE"

**输出：**7

**解释：**

每秒后都有一个顾客进入候诊室，没有人离开。因此，至少需要 7 把椅子。

**示例 2：**

**输入：**s = "ELELEEL"

**输出：**2

**解释：**

假设候诊室里有 2 把椅子。下表显示了每秒钟等候室的状态。

| 秒   | 事件  | 候诊室的人数 | 可用的椅子数 |
| ---- | ----- | ------------ | ------------ |
| 0    | Enter | 1            | 1            |
| 1    | Leave | 0            | 2            |
| 2    | Enter | 1            | 1            |
| 3    | Leave | 0            | 2            |
| 4    | Enter | 1            | 1            |
| 5    | Enter | 2            | 0            |
| 6    | Leave | 1            | 1            |

**示例 3：**

**输入：**s = "ELEELEELLL"

**输出：**3

**解释：**

假设候诊室里有 3 把椅子。下表显示了每秒钟等候室的状态。

| 秒   | 事件  | 候诊室的人数 | 可用的椅子数 |
| ---- | ----- | ------------ | ------------ |
| 0    | Enter | 1            | 2            |
| 1    | Leave | 0            | 3            |
| 2    | Enter | 1            | 2            |
| 3    | Enter | 2            | 1            |
| 4    | Leave | 1            | 2            |
| 5    | Enter | 2            | 1            |
| 6    | Enter | 3            | 0            |
| 7    | Leave | 2            | 1            |
| 8    | Leave | 1            | 2            |
| 9    | Leave | 0            | 3            |

 

**提示：**

- `1 <= s.length <= 50`
- `s` 仅由字母 `'E'` 和 `'L'` 组成。
- `s` 表示一个有效的进出序列。



#### 分析

比较经典的PV操作，遍历所有的操作，取最大值即可

#### 代码

```python
class Solution:
    def minimumChairs(self, s: str) -> int:
        res, p = 0, 0
        for i in s:
            p += i == 'E'
            p -= i == 'L'
            res = max(res, p)
        return res
```



------

### 题目二、[无需开会的工作日](https://leetcode.cn/contest/weekly-contest-400/problems/count-days-without-meetings/)【中等】

#### 题目描述

给你一个正整数 `days`，表示员工可工作的总天数（从第 1 天开始）。另给你一个二维数组 `meetings`，长度为 `n`，其中 `meetings[i] = [start_i, end_i]` 表示第 `i` 次会议的开始和结束天数（包含首尾）。

返回员工可工作且没有安排会议的天数。

**注意：**会议时间可能会有重叠。

 

**示例 1：**

**输入：**days = 10, meetings = [[5,7],[1,3],[9,10]]

**输出：**2

**解释：**

第 4 天和第 8 天没有安排会议。

**示例 2：**

**输入：**days = 5, meetings = [[2,4],[1,3]]

**输出：**1

**解释：**

第 5 天没有安排会议。

**示例 3：**

**输入：**days = 6, meetings = [[1,6]]

**输出：**0

**解释：**

所有工作日都安排了会议。

 

**提示：**

- `1 <= days <= 10^9`
- `1 <= meetings.length <= 10^5`
- `meetings[i].length == 2`
- `1 <= meetings[i][0] <= meetings[i][1] <= days`



#### 分析

将会议时间进行排序，然后记录上一个会议的结束时间：

1.如果上一个会议的结束时间小于下一个会议的开始时间，则它们之间的时间差就是无需开会的工作日。

2.如果上一个会议的结束时间大于下一个会议的开始时间，则取两者的结束时间大的为结束时间。



#### 代码

```Python
class Solution:
    def countDays(self, days: int, meetings: List[List[int]]) -> int:
        meetings.sort()
        res, pre = 0, 0
        for start, end in meetings:
            if start > pre:
                res += start - pre - 1
            pre = max(pre, end)
        res += days - pre
        return res
```

------

### 题目三、[删除星号以后字典序最小的字符串](https://leetcode.cn/contest/weekly-contest-400/problems/lexicographically-minimum-string-after-removing-stars/)【中等】

#### 题目描述

给你一个字符串 `s` 。它可能包含任意数量的 `'*'` 字符。你的任务是删除所有的 `'*'` 字符。

当字符串还存在至少一个 `'*'` 字符时，你可以执行以下操作：

- 删除最左边的 `'*'` 字符，同时删除该星号字符左边一个字典序 **最小** 的字符。如果有多个字典序最小的字符，你可以删除它们中的任意一个。

请你返回删除所有 `'*'` 字符以后，剩余字符连接而成的 字典序最小 的字符串。

 

**示例 1：**

**输入：**s = "aaba*"

**输出：**"aab"

**解释：**

删除 `'*'` 号和它左边的其中一个 `'a'` 字符。如果我们选择删除 `s[3]` ，`s` 字典序最小。

**示例 2：**

**输入：**s = "abc"

**输出：**"abc"

**解释：**

字符串中没有 `'*'` 字符。

 

**提示：**

- `1 <= s.length <= 10^5`
- `s` 只含有小写英文字母和 `'*'` 字符。
- 输入保证操作可以删除所有的 `'*'` 字符。

#### 分析

贪心，删除*左边最近的字典序最小的字符即可。

1.创建一个26个元素的数组arr，arr数组中的每个元素是一个列表，该列表记录每个字符在字符串中出现的位置）。

2.遍历字符串：

​	如果字符不是*则在arr中记录字符的索引

​	如果字符是*，则遍历arr找到字典序最小的字符，并且从该字符的列表中pop出索引最大的索引 ，将该索引和星号的索引加入到删除的索引集合中

3.将不在删除索引集合的字符拼接成字符串

#### 代码

```python
class Solution:
    def clearStars(self, s: str) -> str:
        arr = [[] for _ in range(26)]
        delete = set()
        for i, c in enumerate(s):
            if c != '*':
                arr[ord(c) - ord('a')].append(i)
                continue
                
            delete.add(i)
            
            for p in arr:
                if p:
                    delete.add(p.pop())
                    break
        
        res = "".join(s[i] for i in range(len(s)) if i not in delete)
 
        return res
```

------

### 题目四、【困难】

#### 题目描述



#### 分析



#### 代码

```python

```

