**本文主要解析LeetCode在2024年9月22日10:30组织的第【416】场周赛题目，**[**竞赛链接**](https://leetcode.cn/contest/weekly-contest-416)**。**



### 题目一、[举报垃圾信息](https://leetcode.cn/contest/weekly-contest-416/problems/report-spam-message/)【4分】

给你一个字符串数组 `message` 和一个字符串数组 `bannedWords`。

如果数组中 **至少** 存在两个单词与 `bannedWords` 中的任一单词 **完全相同**，则该数组被视为 **垃圾信息**。

如果数组 `message` 是垃圾信息，则返回 `true`；否则返回 `false`。

 

**示例 1：**

**输入：** message = ["hello","world","leetcode"], bannedWords = ["world","hello"]

**输出：** true

**解释：**

数组 `message` 中的 `"hello"` 和 `"world"` 都出现在数组 `bannedWords` 中。

**示例 2：**

**输入：** message = ["hello","programming","fun"], bannedWords = ["world","programming","leetcode"]

**输出：** false

**解释：**

数组 `message` 中只有一个单词（`"programming"`）出现在数组 `bannedWords` 中。

 

**提示：**

- `1 <= message.length, bannedWords.length <= 10^5`
- `1 <= message[i].length, bannedWords[i].length <= 15`
- `message[i]` 和 `bannedWords[i]` 都只由小写英文字母组成。



#### 分析

模拟题，将bannedWords的所有字符串放在set中，然后遍历message，统计所有在set中存在的单词数量，返回数量是否大于2即可。

时间复杂度O(n)。

#### 代码

```cpp
class Solution {
public:
    bool reportSpam(vector<string>& message, vector<string>& bannedWords) {
        unordered_set<string> b_set(bannedWords.begin(), bannedWords.end());
        int cnt = 0;
        for(auto m : message)
        {
            if(b_set.find(m) != b_set.end()) cnt++;
        }

        return cnt >= 2;
    }
};
```



## 题目二、[移山所需的最少秒数](https://leetcode.cn/contest/weekly-contest-416/problems/minimum-number-of-seconds-to-make-mountain-height-zero/)【5分】

给你一个整数 `mountainHeight` 表示山的高度。

同时给你一个整数数组 `workerTimes`，表示工人们的工作时间（单位：**秒**）。

工人们需要 **同时** 进行工作以 **降低** 山的高度。对于工人 `i` :

- 山的高度降低x，需要花费`workerTimes[i] + workerTimes[i] * 2 + ... + workerTimes[i] * x`秒。例如：
  - 山的高度降低 1，需要 `workerTimes[i]` 秒。
  - 山的高度降低 2，需要 `workerTimes[i] + workerTimes[i] * 2` 秒，依此类推。

返回一个整数，表示工人们使山的高度降低到 0 所需的 **最少** 秒数。

 

**示例 1：**

**输入：** mountainHeight = 4, workerTimes = [2,1,1]

**输出：** 3

**解释：**

将山的高度降低到 0 的一种方式是：

- 工人 0 将高度降低 1，花费 `workerTimes[0] = 2` 秒。
- 工人 1 将高度降低 2，花费 `workerTimes[1] + workerTimes[1] * 2 = 3` 秒。
- 工人 2 将高度降低 1，花费 `workerTimes[2] = 1` 秒。

因为工人同时工作，所需的最少时间为 `max(2, 3, 1) = 3` 秒。

**示例 2：**

**输入：** mountainHeight = 10, workerTimes = [3,2,2,4]

**输出：** 12

**解释：**

- 工人 0 将高度降低 2，花费 `workerTimes[0] + workerTimes[0] * 2 = 9` 秒。
- 工人 1 将高度降低 3，花费 `workerTimes[1] + workerTimes[1] * 2 + workerTimes[1] * 3 = 12` 秒。
- 工人 2 将高度降低 3，花费 `workerTimes[2] + workerTimes[2] * 2 + workerTimes[2] * 3 = 12` 秒。
- 工人 3 将高度降低 2，花费 `workerTimes[3] + workerTimes[3] * 2 = 12` 秒。

所需的最少时间为 `max(9, 12, 12, 12) = 12` 秒。

**示例 3：**

**输入：** mountainHeight = 5, workerTimes = [1]

**输出：** 15

**解释：**

这个示例中只有一个工人，所以答案是 `workerTimes[0] + workerTimes[0] * 2 + workerTimes[0] * 3 + workerTimes[0] * 4 + workerTimes[0] * 5 = 15` 秒。

 

**提示：**

- `1 <= mountainHeight <= 10^5`
- `1 <= workerTimes.length <= 10^4`
- `1 <= workerTimes[i] <= 10^6`



#### 分析

假设秒数为x能完成工作，那么秒数为x+1肯定能完成工作，所以秒数具有单调性，可以使用二分法进行处理，本题是二分套二分。

第一步：二分秒数，检查在某个秒数下是否可以完成任务: 遍历所有工人，求出每个工人能够下降的高度，判断该下降高度的总和是否大于等于mountainHeight。

第二步：需要求在指定的秒数下工人能够降低的高度，用二分法求出最大的高度。

**小技巧：**
$$
workerTimes[i] + workerTimes[i] * 2 + ... + workerTimes[i] * x`
$$
是一个等差数列，等差数列求和可以使用下面这个公式：
$$
(workerTimes[i] + workerTimes[i] * x) * x / 2
$$
等价于：
$$
workerTimes[i] *(1 + x) * x / 2
$$

#### 代码

```cpp
class Solution {
typedef long long LL; 
public:
    // 二分法获取总时间为totalTime时，工人能降低多少高度
    LL getHeight(LL totalTime, int time)
    {
        __int128 l = 0, r = totalTime;
        while(l < r)
        {
            __int128 mid = (l + r) >> 1;
            if(((mid+1) * mid  / 2) * time <= totalTime) l = mid + 1;
            else r = mid - 1;
        }
        if((l+1) * l * time / 2 <= totalTime) return l;
        return l - 1;
    }

    // 总时间为totalTime时，所有工人同时工作能否完成工作
    bool check(LL totalTime, int mountainHeight, vector<int>& workerTimes)
    {
        int height = 0;
        for(int time : workerTimes)
        {
            height += getHeight(totalTime, time);
            if(height >= mountainHeight) return true;
        }

        return false;
    }

    long long minNumberOfSeconds(int mountainHeight, vector<int>& workerTimes) {
        LL l = 0, r = (workerTimes[0] + (LL)workerTimes[0] * mountainHeight) * mountainHeight / 2;
        //
        while(l < r) 
        {
            LL mid = (l + r) >> 1;
            if(check(mid, mountainHeight ,workerTimes)) r = mid - 1;
            else l = mid + 1;
        }

        if(check(r, mountainHeight, workerTimes)) return r;
        return r + 1;
    }
};
```



### 题目三、[统计重新排列后包含另一个字符串的子字符串数目 I](https://leetcode.cn/contest/weekly-contest-416/problems/count-substrings-that-can-be-rearranged-to-contain-a-string-i/)【5分】

给你两个字符串 `word1` 和 `word2` 。

如果一个字符串 `x` 重新排列后，`word2` 是重排字符串的 前缀，那么我们称字符串 `x` 是 **合法的** 。

请你返回 `word1` 中 **合法** 子字符串的数目。



**示例 1：**

**输入：**word1 = "bcca", word2 = "abc"

**输出：**1

**解释：**

唯一合法的子字符串是 `"bcca"` ，可以重新排列得到 `"abcc"` ，`"abc"` 是它的前缀。

**示例 2：**

**输入：**word1 = "abcabc", word2 = "abc"

**输出：**10

**解释：**

除了长度为 1 和 2 的所有子字符串都是合法的。

**示例 3：**

**输入：**word1 = "abcabc", word2 = "aaabc"

**输出：**0

 

**解释：**

- `1 <= word1.length <= 10^5`
- `1 <= word2.length <= 10^4`
- `word1` 和 `word2` 都只包含小写英文字母。



**题目三和题目四题面是一样的，只有数据多了一个量级，所以放在题目四一起分析和讨论**



### 题目四、[统计重新排列后包含另一个字符串的子字符串数目 II](https://leetcode.cn/contest/weekly-contest-416/problems/count-substrings-that-can-be-rearranged-to-contain-a-string-ii/)【6分】

给你两个字符串 `word1` 和 `word2` 。

如果一个字符串 `x` 重新排列后，`word2` 是重排字符串的前缀，那么我们称字符串 `x` 是 **合法的** 。



请你返回 `word1` 中 **合法** 

子字符串

 的数目。



**注意** ，这个问题中的内存限制比其他题目要 **小** ，所以你 **必须** 实现一个线性复杂度的解法。

 

**示例 1：**

**输入：**word1 = "bcca", word2 = "abc"

**输出：**1

**解释：**

唯一合法的子字符串是 `"bcca"` ，可以重新排列得到 `"abcc"` ，`"abc"` 是它的前缀。

**示例 2：**

**输入：**word1 = "abcabc", word2 = "abc"

**输出：**10

**解释：**

除了长度为 1 和 2 的所有子字符串都是合法的。

**示例 3：**

**输入：**word1 = "abcabc", word2 = "aaabc"

**输出：**0

 

**解释：**

- `1 <= word1.length <= 10^6`
- `1 <= word2.length <= 10^4`
- `word1` 和 `word2` 都只包含小写英文字母。



#### 分析

滑动窗口：窗口内不包含word2时，r往前移动，直到窗口内包含word2的所有字符，当窗口内包含所有字符时，l往前移动，直到窗口内不包含word2的所有字符。假设l往前移动t步，则此次子序列数目为N * (n - r).



#### 代码

```cpp
class Solution {
typedef long long LL;
public:
    int target[26], arr[26];
    bool check()
    {
        for(int i=0;i<26;i++)
        {
            if(arr[i] < target[i]) return false; 
        }
        return true;
    }

    long long validSubstringCount(string word1, string word2) {
        memset(target, 0, sizeof target);
        memset(arr, 0, sizeof arr);
        for(int i=0;i<word2.size();i++) target[word2[i] - 'a']++;

        int l =0, r=0,n=word1.size();
        long long res = 0;
        while(r < n)
        {
            arr[word1[r]- 'a']++;
            if(!check()) {
                r++;
                continue;
            }

            while(check())
            {
                res += n - r;
                arr[word1[l++] - 'a']--;
            }
            r++;
        }

        return res;
    }
};
```







