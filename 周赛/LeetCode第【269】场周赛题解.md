

###### 本文主要解析LeetCode在2021年11月28日10：30组织的第【269】场周赛题目，[竞赛链接](https://leetcode-cn.com/contest/weekly-contest-269)。

###### 有兴趣的同学可以关注一下我的LeetCode[个人账号](https://leetcode-cn.com/u/chen-xiao-bin-5/)。

###### 周赛群人数过多，只能通过邀请进群，有兴趣一起打周赛的同学可以添加我的微信号：cbbdwx，拉你进群

------

### 题目一、[5938. 找出数组排序后的目标下标](https://leetcode-cn.com/problems/find-target-indices-after-sorting-array/)【简单】

#### 题目描述

> 给你一个下标从 0 开始的整数数组 nums 以及一个目标元素 target 。
>
> 目标下标 是一个满足 nums[i] == target 的下标 i 。
>
> 将 nums 按 **非递减** 顺序排序后，返回由 nums 中目标下标组成的列表。如果不存在目标下标，返回一个 **空** 列表。返回的列表必须按 **递增** 顺序排列。
>

#### 示例 1

> 输入：nums = [1,2,5,2,3], target = 2
>
> 输出：[1,2]
>
> 解释：排序后，nums 变为 [1,2,2,3,5] 。
>
> 满足 nums[i] == 2 的下标是 1 和 2 。

#### 示例 2

> 输入：nums = [1,2,5,2,3], target = 3
>
> 输出：[3]
>
> 解释：排序后，nums 变为 [1,2,2,3,5] 。
>
> 满足 nums[i] == 3 的下标是 3 。

#### 示例 3

> 输入：nums = [1,2,5,2,3], target = 5
>
> 输出：[4]
>
> 解释：排序后，nums 变为 [1,2,2,3,5] 。
>
> 满足 nums[i] == 5 的下标是 4 。

#### 示例 4

> 输入：nums = [1,2,5,2,3], target = 4
>
> 输出：[]
>
> 解释：nums 中不含值为 4 的元素。

#### 提示

> 1 <= nums.length <= 100
> 1 <= nums[i], target <= 100

#### 分析

简单模拟题，按照题目意思先排序，再通过遍历找到与target相同的值的下标即可，也可以使用二分法降低时间复杂度。

#### 代码

```java
class Solution {
    public List<Integer> targetIndices(int[] nums, int target) {
        Arrays.sort(nums);
        List<Integer> list = new ArrayList<>();
        for(int i=0;i<nums.length;i++) {
            if(nums[i] == target) {
                list.add(i);
            }

            if(nums[i] > target) break;
        }
        
        return list;
    }
}
```



------

### 题目二、[5939. 半径为 k 的子数组平均值](https://leetcode-cn.com/problems/k-radius-subarray-averages/)【中等】

#### 题目描述

> 给你一个下标从 0 开始的数组 nums ，数组中有 n 个整数，另给你一个整数 k 。
>
> **半径为 k 的子数组平均值** 是指：nums 中一个以下标 i 为 **中心** 且**半径** 为 k 的子数组中所有元素的平均值，即下标在 i - k 和 i + k 范围（**含** i - k 和 i + k）内所有元素的平均值。如果在下标 i 前或后不足 k 个元素，那么 **半径为 k 的子数组平均值** 是 -1 。
>
> 构建并返回一个长度为 n 的数组 avgs ，其中 avgs[i] 是以下标 i 为中心的子数组的 **半径为 k 的子数组平均值** 。
>
> x 个元素的 **平均值** 是 x 个元素相加之和除以 x ，此时使用截断式 **整数除法** ，即需要去掉结果的小数部分。
>
> 
>
> 例如，四个元素 2、3、1 和 5 的平均值是 (2 + 3 + 1 + 5) / 4 = 11 / 4 = 3.75，截断后得到 3 。

#### 示例 1

> 输入：nums = [7,4,3,9,1,8,5,2,6], k = 3
>
> 输出：[-1,-1,-1,5,4,4,-1,-1,-1]
>
> 解释：
>
> - avg[0]、avg[1] 和 avg[2] 是 -1 ，因为在这几个下标前的元素数量都不足 k 个。
> - 中心为下标 3 且半径为 3 的子数组的元素总和是：7 + 4 + 3 + 9 + 1 + 8 + 5 = 37 。
>   使用截断式 整数除法，avg[3] = 37 / 7 = 5 。
> - 中心为下标 4 的子数组，avg[4] = (4 + 3 + 9 + 1 + 8 + 5 + 2) / 7 = 4 。
> - 中心为下标 5 的子数组，avg[5] = (3 + 9 + 1 + 8 + 5 + 2 + 6) / 7 = 4 。
> - avg[6]、avg[7] 和 avg[8] 是 -1 ，因为在这几个下标后的元素数量都不足 k 个。
>

#### 示例2

> 输入：nums = [100000], k = 0
>
> 输出：[100000]
>
> 解释：
>
> - 中心为下标 0 且半径 0 的子数组的元素总和是：100000 。
>   avg[0] = 100000 / 1 = 100000 。
>

#### 示例3

> 输入：nums = [8], k = 100000
>
> 输出：[-1]
>
> 解释：
>
> - avg[0] 是 -1 ，因为在下标 0 前后的元素数量均不足 k 。
>

#### 提示

> n == nums.length
>
> 1 <= n <= 10^5
>
> 0 <= nums[i], k <= 10^5

#### 分析

本题需要求数组中一段连续元素的和，可以使用前缀和，注意本题由于有10^5个元素，并且nums[i]<= 10^5，所以所有数字的和可能达到10^10，java中int最大值是2147483648，所以前缀和数组的类型使用int时，可能会超出数据范围，前缀和数组的类型应该使用long。

#### 代码

```java
class Solution {
    public int[] getAverages(int[] nums, int k) {
        int n = nums.length;
        long[] preSum = new long[n];
        preSum[0] = nums[0];
        for(int i=1;i<n;i++) {
            preSum[i] = preSum[i-1] + nums[i];
        }
        
        int[] result = new int[n];
        
        for(int i=0;i<n;i++) {
            if(i -k < 0 || i+k>=n) result[i] = -1;
            else result[i] = (int)((preSum[i+k] - preSum[i-k] + nums[i-k]) / (2 * k + 1)); 
        }
        
        return result;
    }
}
```



------



### 题目三、[5940. 从数组中移除最大值和最小值](https://leetcode-cn.com/problems/removing-minimum-and-maximum-from-array/)【中等】

#### 题目描述

> 给你一个下标从 **0** 开始的数组 nums ，数组由若干 **互不相同** 的整数组成。
>
> nums 中有一个值最小的元素和一个值最大的元素。分别称为 **最小值** 和 **最大值** 。你的目标是从数组中移除这两个元素。
>
> 一次 **删除** 操作定义为从数组的 **前面** 移除一个元素或从数组的 **后面** 移除一个元素。
>
> 返回将数组中最小值和最大值 **都** 移除需要的最小删除次数。
>

#### 示例 1

> 输入：nums = [2,10,7,5,4,1,8,6]
>
> 输出：5
>
> 解释：
> 数组中的最小元素是 nums[5] ，值为 1 。
> 数组中的最大元素是 nums[1] ，值为 10 。
> 将最大值和最小值都移除需要从数组前面移除 2 个元素，从数组后面移除 3 个元素。
> 结果是 2 + 3 = 5 ，这是所有可能情况中的最小删除次数。

#### 示例 2

> 输入：nums = [0,-4,19,1,8,-2,-3,5]
>
> 输出：3
>
> 解释：
> 数组中的最小元素是 nums[1] ，值为 -4 。
> 数组中的最大元素是 nums[2] ，值为 19 。
> 将最大值和最小值都移除需要从数组前面移除 3 个元素。
> 结果是 3 ，这是所有可能情况中的最小删除次数。 

#### 示例 3

> 输入：nums = [101]
>
> 输出：1
>
> 解释：
> 数组中只有这一个元素，那么它既是数组中的最小值又是数组中的最大值。
> 移除它只需要 1 次删除操作。

#### 提示

> 1 <= nums.length <= 10^5
>
> -10^5 <= nums[i] <= 10^5
>
> nums 中的整数 互不相同

#### 分析

模拟题，解题步骤：

1.先找到最大值和最小值的坐标；

2.算出从左边开始删除需要的删除次数、从右边删除的次数和从左右两边删除的次数；

3.返回最少的次数。

#### 代码

```java
class Solution {
    public int minimumDeletions(int[] nums) {
        int n = nums.length;
        if(n <= 2) return n;
        
        int minIndex = 0, min = nums[0];
        int maxIndex = 0, max = nums[0];
        
        //求出最大值和最小值的坐标
        for(int i=0;i<n;i++) {
            int val = nums[i];
            if(val < min) {
                minIndex = i;
                min = val;
            }
            
            if(val > max) {
                maxIndex = i;
                max = val;
            }
        }
        
        int l = Math.min(minIndex, maxIndex), r = Math.max(minIndex, maxIndex);
        
        //从左边删除
        int result = r + 1;
        //从右边删除
        result = Math.min(result, n - l);
        //左右两边同时删除
        result = Math.min(result, l + 1 + n - r);
        
        return result;  
    }
}
```



------



#### 题目四、[5941. 找出知晓秘密的所有专家](https://leetcode-cn.com/problems/find-all-people-with-secret/)【困难】

#### 题目描述

> 给你一个整数 n ，表示有 n 个专家从 0 到 n - 1 编号。另外给你一个下标从 0 开始的二维整数数组 meetings ，其中 meetings[i] = [xi, yi, timei] 表示专家 xi 和专家 yi 在时间 timei 要开一场会。一个专家可以同时参加 多场会议 。最后，给你一个整数 firstPerson 。
>
> 专家 0 有一个 秘密 ，最初，他在时间 0 将这个秘密分享给了专家 firstPerson 。接着，这个秘密会在每次有知晓这个秘密的专家参加会议时进行传播。更正式的表达是，每次会议，如果专家 xi 在时间 timei 时知晓这个秘密，那么他将会与专家 yi 分享这个秘密，反之亦然。
>
> 秘密共享是 **瞬时发生** 的。也就是说，在同一时间，一个专家不光可以接收到秘密，还能在其他会议上与其他专家分享。
>
> 在所有会议都结束之后，返回所有知晓这个秘密的专家列表。你可以按 任何顺序 返回答案。
>

#### 示例 1

> 输入：n = 6, meetings = [[1,2,5],[2,3,8],[1,5,10]], firstPerson = 1
>
> 输出：[0,1,2,3,5]
>
> 解释：
> 时间 0 ，专家 0 将秘密与专家 1 共享。
> 时间 5 ，专家 1 将秘密与专家 2 共享。
> 时间 8 ，专家 2 将秘密与专家 3 共享。
> 时间 10 ，专家 1 将秘密与专家 5 共享。
> 因此，在所有会议结束后，专家 0、1、2、3 和 5 都将知晓这个秘密。

#### 示例 2

> 输入：n = 4, meetings = [[3,1,3],[1,2,2],[0,3,3]], firstPerson = 3
>
> 输出：[0,1,3]
>
> 解释：
> 时间 0 ，专家 0 将秘密与专家 3 共享。
> 时间 2 ，专家 1 与专家 2 都不知晓这个秘密。
> 时间 3 ，专家 3 将秘密与专家 0 和专家 1 共享。
> 因此，在所有会议结束后，专家 0、1 和 3 都将知晓这个秘密。

#### 示例 3

> 输入：n = 5, meetings = [[3,4,2],[1,2,1],[2,3,1]], firstPerson = 1
>
> 输出：[0,1,2,3,4]
>
> 解释：
> 时间 0 ，专家 0 将秘密与专家 1 共享。
> 时间 1 ，专家 1 将秘密与专家 2 共享，专家 2 将秘密与专家 3 共享。
> 注意，专家 2 可以在收到秘密的同一时间分享此秘密。
> 时间 2 ，专家 3 将秘密与专家 4 共享。
> 因此，在所有会议结束后，专家 0、1、2、3 和 4 都将知晓这个秘密。

#### 示例 4

> 输入：n = 6, meetings = [[0,2,1],[1,3,1],[4,5,1]], firstPerson = 1
>
> 输出：[0,1,2,3]
>
> 解释：
> 时间 0 ，专家 0 将秘密与专家 1 共享。
> 时间 1 ，专家 0 将秘密与专家 2 共享，专家 1 将秘密与专家 3 共享。
> 因此，在所有会议结束后，专家 0、1、2 和 3 都将知晓这个秘密。

#### 提示

> 2 <= n <= 10^5
>
> 1 <= meetings.length <= 10^5
>
> meetings[i].length == 3
>
> 0 <= xi, yi <= n - 1
>
> xi != yi
>
> 1 <= timei <= 10^5
>
> 1 <= firstPerson <= n - 1

#### 分析

本题是求连通性的问题，可以使用并查集解决。

本题的难点就在于秘密分享是同时发生的，如果单纯通过遍历可能会导致忽略前面的会议，比如：

示例3：

输入：n = 5, meetings = [[3,4,2],[1,2,1],[2,3,1]], firstPerson = 1

按照时间将会议分成两组

1:[2,3,1]、[1,2,1]

2:[3,4,2]



按照时间线分析

时间0

知道秘密的人：[0,1]



时间1：

如果处理[2,3,1]这个会议，此时2和3都不知道秘密

再处理[1,2,1]，此时由于1知道秘密，所以2也知道秘密

所以时间1过后，知道秘密的人是[0,1,2]



但是时间1结束之后正确的结果是[0,1,2,3]，因为2知道秘密的同时会通过会议[2,3,1]将秘密告诉3，所以单纯的通过遍历有可能会忽略前面的会议。



解决方案：

我们遍历的时候如果两个人都不知道秘密，那么将这两个人连通在一起。

比如时间1：

处理[2,3,1]这个会议时，由于2和3都不知道秘密，所以将2和3连通在一起

处理[1,2,1]这个会议时，由于1知道秘密，所以将1和2连通到0，此时根据并查集的特点，3会自动连通到0

所以这个时间过后，知道秘密的人：[0,1,2,3]



假设，我们的例子中没有后面这个[1,2,1]会议，因为时间1结束了，下一个时间点2和3不一定有会议，所以需要将2和3的连通性解开。



在原有的并查集模板上需要新增一个解开连通性的方法split(int x)，并查集模板：

```java
   private class UnionFind{
        int[] parent=null;
        int count = 0;

        public UnionFind(int n) {
            parent = new int[n];
            for(int i=0;i<n;i++) {
                parent[i] = i;
            }
            count = n;
        }

        public int find(int n) {
            while(n != parent[n]) {
                parent[n] = parent[parent[n]];

                n = parent[n];
            }
            return n;
        }

				//解开连通性
        public void split(int x) {
            parent[x] = x;
        }

        public boolean isConnected(int x, int y) {
            return find(x) == find(y);
        }

        public void union(int x, int y) {
            int xf = find(x);
            int yf = find(y);
            if(xf == yf) return;
            parent[xf] = yf;
            count--;
        }
    }
```



#### 代码

```java
class Solution {
    public List<Integer> findAllPeople(int n, int[][] meetings, int firstPerson) {
    		//将会议按照时间归并在一起，并且按照从小到大排序
        TreeMap<Integer, List<int[]>> map = new TreeMap<>();
        for(int[] meeting : meetings) {
            int time = meeting[2];
            List<int[]> list = map.getOrDefault(time, new ArrayList<>());
            list.add(meeting);
            map.put(time, list);
        }
        
        UnionFind uf = new UnionFind(n);
        uf.union(0,firstPerson);

        for(Map.Entry<Integer, List<int[]>> entry : map.entrySet()) {
            List<int[]> list = entry.getValue();
            //遍历每个会议，如果会议中有人知道秘密，则将该会议的所有人跟0进行union
            for(int[] meeting : list) {
                if(uf.isConnected(0,meeting[0]) || uf.isConnected(0,meeting[1])) {
                    uf.union(0, meeting[0]);
                    uf.union(0, meeting[1]);
                }
								
								//连通会议中的两人
                uf.union(meeting[0], meeting[1]);
            }
						
						//再次遍历所有会议，如果会议中的人都不知道秘密，则将会议中的两个人的连通性解开
            for(int[] meeting : list) {
                if(!uf.isConnected(0,meeting[0]) && !uf.isConnected(0,meeting[1])) {
                    uf.split(meeting[0]);
                    uf.split(meeting[1]);
                }
            }
        }
        
        List<Integer> list = new ArrayList<>();
        for(int i=0;i<n;i++) {
            if(uf.isConnected(0, i)) list.add(i);
        }
        
        return list;
    }

    
    private class UnionFind{
        int[] parent=null;
        int count = 0;

        public UnionFind(int n) {
            parent = new int[n];
            for(int i=0;i<n;i++) {
                parent[i] = i;
            }
            count = n;
        }

        public int find(int n) {
            while(n != parent[n]) {
                parent[n] = parent[parent[n]];

                n = parent[n];
            }
            return n;
        }

        public void split(int x) {
            parent[x] = x;
        }

        public boolean isConnected(int x, int y) {
            return find(x) == find(y);
        }

        public void union(int x, int y) {
            int xf = find(x);
            int yf = find(y);
            if(xf == yf) return;
            parent[xf] = yf;
            count--;
        }
    }
}
```

