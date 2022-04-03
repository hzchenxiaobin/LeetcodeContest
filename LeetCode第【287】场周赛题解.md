### 题目一、[6055. 转化时间需要的最少操作数](https://leetcode-cn.com/problems/minimum-number-of-operations-to-convert-time/)【简单】

给你两个字符串 `current` 和 `correct` ，表示两个 **24 小时制时间** 。

**24 小时制时间** 按 `"HH:MM"` 进行格式化，其中 `HH` 在 `00` 和 `23` 之间，而 `MM` 在 `00` 和 `59` 之间。最早的 24 小时制时间为 `00:00` ，最晚的是 `23:59` 。

在一步操作中，你可以将 `current` 这个时间增加 `1`、`5`、`15` 或 `60` 分钟。你可以执行这一操作 **任意** 次数。

返回将 `current` 转化为 `correct` 需要的 **最少操作数** 。

 

**示例 1：**

```
输入：current = "02:30", correct = "04:35"
输出：3
解释：
可以按下述 3 步操作将 current 转换为 correct ：
- 为 current 加 60 分钟，current 变为 "03:30" 。
- 为 current 加 60 分钟，current 变为 "04:30" 。 
- 为 current 加 5 分钟，current 变为 "04:35" 。
可以证明，无法用少于 3 步操作将 current 转化为 correct 。
```

**示例 2：**

```
输入：current = "11:00", correct = "11:01"
输出：1
解释：只需要为 current 加一分钟，所以最小操作数是 1 。
```

 

**提示：**

- `current` 和 `correct` 都符合 `"HH:MM"` 格式
- `current <= correct`



#### 分析

简单题，模拟即可

算出两个时间的分钟数之差，重复以下步骤：

1.如果差大于60，则减60

2.如果差大于15，则减去15

3.如果差大于5，则减去5

4.减去1.



#### 代码

```java
class Solution {
    public int convertTime(String current, String correct) {
        String[] arr1 = current.split(":"), arr2 = correct.split(":");
        int t1 = Integer.parseInt(arr1[0]) * 60 + Integer.parseInt(arr1[1]);
        int t2 = Integer.parseInt(arr2[0]) * 60 + Integer.parseInt(arr2[1]);
        int diff = t2 - t1;
        
        int res = 0;
        while(diff > 0) {
            res++;
            if(diff >= 60) {
                diff -= 60;
            } else if(diff >= 15) {
                diff -= 15;
            } else if(diff >= 5) {
                diff -= 5;
            } else {
                diff--;
            }
        }
        
        return res;
    }
}
```



------



### 题目二、[5235. 找出输掉零场或一场比赛的玩家](https://leetcode-cn.com/problems/find-players-with-zero-or-one-losses/)【中等】

给你一个整数数组 `matches` 其中 `matches[i] = [winneri, loseri]` 表示在一场比赛中 `winneri` 击败了 `loseri` 。

返回一个长度为 2 的列表 `answer` ：

- `answer[0]` 是所有 **没有** 输掉任何比赛的玩家列表。
- `answer[1]` 是所有恰好输掉 **一场** 比赛的玩家列表。

两个列表中的值都应该按 **递增** 顺序返回。

**注意：**

- 只考虑那些参与 **至少一场** 比赛的玩家。
- 生成的测试用例保证 **不存在** 两场比赛结果 **相同** 。

 

**示例 1：**

```
输入：matches = [[1,3],[2,3],[3,6],[5,6],[5,7],[4,5],[4,8],[4,9],[10,4],[10,9]]
输出：[[1,2,10],[4,5,7,8]]
解释：
玩家 1、2 和 10 都没有输掉任何比赛。
玩家 4、5、7 和 8 每个都输掉一场比赛。
玩家 3、6 和 9 每个都输掉两场比赛。
因此，answer[0] = [1,2,10] 和 answer[1] = [4,5,7,8] 。
```

**示例 2：**

```
输入：matches = [[2,3],[1,3],[5,4],[6,4]]
输出：[[1,2,5,6],[]]
解释：
玩家 1、2、5 和 6 都没有输掉任何比赛。
玩家 3 和 4 每个都输掉两场比赛。
因此，answer[0] = [1,2,5,6] 和 answer[1] = [] 。
```

 

**提示：**

- `1 <= matches.length <= 105`
- `matches[i].length == 2`
- `1 <= winneri, loseri <= 105`
- `winneri != loseri`
- 所有 `matches[i]` **互不相同**



#### 分析

统计所有人输掉的场次即可，返回输掉场次为0和输掉场次为1的列表。



#### 代码

```java
class Solution {
    public List<List<Integer>> findWinners(int[][] matches) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int[] match : matches) {
            int winner = match[0];
            int lose = match[1];
            map.put(winner, map.getOrDefault(winner, 0));
            map.put(lose, map.getOrDefault(lose, 0) + 1);
        }
        
        List<Integer> win = new ArrayList<>(), los = new ArrayList<>();
        for(Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if(entry.getValue() == 0) {
                win.add(entry.getKey());
            }
            
            if(entry.getValue() == 1) {
                los.add(entry.getKey());
            }
        }
        
        Collections.sort(win);
        Collections.sort(los);
        List<List<Integer>> res=  new ArrayList<>();
        res.add(win);
        res.add(los);
        return res;
    }
}
```



------

### 题目三、[5219. 每个小孩最多能分到多少糖果](https://leetcode-cn.com/problems/maximum-candies-allocated-to-k-children/)【中等】

给你一个 **下标从 0 开始** 的整数数组 `candies` 。数组中的每个元素表示大小为 `candies[i]` 的一堆糖果。你可以将每堆糖果分成任意数量的 **子堆** ，但 **无法** 再将两堆合并到一起。

另给你一个整数 `k` 。你需要将这些糖果分配给 `k` 个小孩，使每个小孩分到 **相同** 数量的糖果。每个小孩可以拿走 **至多一堆** 糖果，有些糖果可能会不被分配。

返回每个小孩可以拿走的 **最大糖果数目** 。

 

**示例 1：**

```
输入：candies = [5,8,6], k = 3
输出：5
解释：可以将 candies[1] 分成大小分别为 5 和 3 的两堆，然后把 candies[2] 分成大小分别为 5 和 1 的两堆。现在就有五堆大小分别为 5、5、3、5 和 1 的糖果。可以把 3 堆大小为 5 的糖果分给 3 个小孩。可以证明无法让每个小孩得到超过 5 颗糖果。
```

**示例 2：**

```
输入：candies = [2,5], k = 11
输出：0
解释：总共有 11 个小孩，但只有 7 颗糖果，但如果要分配糖果的话，必须保证每个小孩至少能得到 1 颗糖果。因此，最后每个小孩都没有得到糖果，答案是 0 。
```

 

**提示：**

- `1 <= candies.length <= 10^5`
- `1 <= candies[i] <= 10^7`
- `1 <= k <= 10^12`



#### 分析

二分法模板题

每个小孩分到的最多糖果是糖果总数除以k得到的平均值，通过二分法找到满足能分给k个人的最大糖果数，



#### 代码

```java
class Solution {
    public int maximumCandies(int[] candies, long k) {
        long sum = 0L;
        int n = candies.length;
        for(int candy : candies) {
            sum += candy;
        }
        
        if(sum < k) return 0;
        
        int aver = (int)(sum / k);
        int right = aver, left =1;
        while(right > left) {
            int mid = left + (right - left) / 2;
            if(check(candies, k, mid)) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        if(check(candies, k, right)) return right;
        return right - 1;
        
    }
    
    private boolean check(int[] candies, long k, int num) {
        long count = 0l;
        for(int candy : candies) {
            count += candy / num;
        }
        
        return count >= k;
    }
}
```

------

### 题目四、[5302. 加密解密字符串](https://leetcode-cn.com/problems/encrypt-and-decrypt-strings/)【困难】

给你一个字符数组 `keys` ，由若干 **互不相同** 的字符组成。还有一个字符串数组 `values` ，内含若干长度为 2 的字符串。另给你一个字符串数组 `dictionary` ，包含解密后所有允许的原字符串。请你设计并实现一个支持加密及解密下标从 **0** 开始字符串的数据结构。

字符串 **加密** 按下述步骤进行：

1. 对字符串中的每个字符 `c` ，先从 `keys` 中找出满足 `keys[i] == c` 的下标 `i` 。
2. 在字符串中，用 `values[i]` 替换字符 `c` 。

字符串 **解密** 按下述步骤进行：

1. 将字符串每相邻 2 个字符划分为一个子字符串，对于每个子字符串 `s` ，找出满足 `values[i] == s` 的一个下标 `i` 。如果存在多个有效的 `i` ，从中选择 **任意** 一个。这意味着一个字符串解密可能得到多个解密字符串。
2. 在字符串中，用 `keys[i]` 替换 `s` 。

实现 `Encrypter` 类：

- `Encrypter(char[] keys, String[] values, String[] dictionary)` 用 `keys`、`values` 和 `dictionary` 初始化 `Encrypter` 类。
- `String encrypt(String word1)` 按上述加密过程完成对 `word1` 的加密，并返回加密后的字符串。
- `int decrypt(String word2)` 统计并返回可以由 `word2` 解密得到且出现在 `dictionary` 中的字符串数目。

 

**示例：**

```
输入：
["Encrypter", "encrypt", "decrypt"]
[[['a', 'b', 'c', 'd'], ["ei", "zf", "ei", "am"], ["abcd", "acbd", "adbc", "badc", "dacb", "cadb", "cbda", "abad"]], ["abcd"], ["eizfeiam"]]
输出：
[null, "eizfeiam", 2]

解释：
Encrypter encrypter = new Encrypter([['a', 'b', 'c', 'd'], ["ei", "zf", "ei", "am"], ["abcd", "acbd", "adbc", "badc", "dacb", "cadb", "cbda", "abad"]);
encrypter.encrypt("abcd"); // 返回 "eizfeiam"。 
                           // 'a' 映射为 "ei"，'b' 映射为 "zf"，'c' 映射为 "ei"，'d' 映射为 "am"。
encrypter.decrypt("eizfeiam"); // return 2. 
                              // "ei" 可以映射为 'a' 或 'c'，"zf" 映射为 'b'，"am" 映射为 'd'。 
                              // 因此，解密后可以得到的字符串是 "abad"，"cbad"，"abcd" 和 "cbcd"。 
                              // 其中 2 个字符串，"abad" 和 "abcd"，在 dictionary 中出现，所以答案是 2 。
```

 

**提示：**

- `1 <= keys.length == values.length <= 26`
- `values[i].length == 2`
- `1 <= dictionary.length <= 100`
- `1 <= dictionary[i].length <= 100`
- 所有 `keys[i]` 和 `dictionary[i]` **互不相同**
- `1 <= word1.length <= 2000`
- `1 <= word2.length <= 200`
- 所有 `word1[i]` 都出现在 `keys` 中
- `word2.length` 是偶数
- `keys`、`values[i]`、`dictionary[i]`、`word1` 和 `word2` 只含小写英文字母
- 至多调用 `encrypt` 和 `decrypt` **总计** `200` 次



#### 分析

阅读理解题。

加密比较简单。

解密如果从正向去想，将word2解密出来，再判断所有的结果在dictionary中的数量，会超出时间限制。

考虑到dictionary中元素的数量只有100个，将dictionary中所有的字符串进行加密，如果加密的结果与word2相等，则数量加一。



#### 代码

```java
class Encrypter {

    Map<Character, String> map = new HashMap<>();    
    String[] dictionary;
    
    public Encrypter(char[] keys, String[] values, String[] dictionary) {
       for(int i=0;i<keys.length;i++) {
           map.put(keys[i], values[i]);
       }
        this.dictionary = dictionary;
    }
    
    public String encrypt(String word1) {
        StringBuilder sb = new StringBuilder();
        for(int i=0;i<word1.length();i++) {
            sb.append(map.get(word1.charAt(i)));
        }
        
        return sb.toString();
    }
    
    public int decrypt(String word2) {
        int res = 0;
        for(String str : dictionary) {
            if(check(str, word2)) res++;
        }
        
        return res;
    }
    
    private boolean check(String s, String o) {
        StringBuilder sb = new StringBuilder();
        for(int i=0;i<s.length();i++) {
            sb.append(map.get(s.charAt(i)));
        }
        
        return (sb.toString()).equals(o);
    }
}

/**
 * Your Encrypter object will be instantiated and called as such:
 * Encrypter obj = new Encrypter(keys, values, dictionary);
 * String param_1 = obj.encrypt(word1);
 * int param_2 = obj.decrypt(word2);
 */
```



