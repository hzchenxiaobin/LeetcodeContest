### 题目一、[6124. 第一个出现两次的字母](https://leetcode.cn/problems/first-letter-to-appear-twice/)【简单】

给你一个由小写英文字母组成的字符串 `s` ，请你找出并返回第一个出现 **两次** 的字母。

**注意：**

- 如果 `a` 的 **第二次** 出现比 `b` 的 **第二次** 出现在字符串中的位置更靠前，则认为字母 `a` 在字母 `b` 之前出现两次。
- `s` 包含至少一个出现两次的字母。

 

**示例 1：**

```
输入：s = "abccbaacz"
输出："c"
解释：
字母 'a' 在下标 0 、5 和 6 处出现。
字母 'b' 在下标 1 和 4 处出现。
字母 'c' 在下标 2 、3 和 7 处出现。
字母 'z' 在下标 8 处出现。
字母 'c' 是第一个出现两次的字母，因为在所有字母中，'c' 第二次出现的下标是最小的。
```

**示例 2：**

```
输入：s = "abcdd"
输出："d"
解释：
只有字母 'd' 出现两次，所以返回 'd' 。
```

 

**提示：**

- `2 <= s.length <= 100`
- `s` 由小写英文字母组成
- `s` 包含至少一个重复字母



#### 分析

简单题，模拟即可



#### 代码

```java
class Solution {
    public char repeatedCharacter(String s) {
        Set<Character> set = new HashSet<>();
        for(int i=0;;i++) {
            char c = s.charAt(i);
            if(!set.add(c)) return c;
        }
    }
}
```

------

### 题目二、[6125. 相等行列对](https://leetcode.cn/problems/equal-row-and-column-pairs/)【中等】

给你一个下标从 **0** 开始、大小为 `n x n` 的整数矩阵 `grid` ，返回满足 `Ri` 行和 `Cj` 列相等的行列对 `(Ri, Cj)` 的数目*。*

如果行和列以相同的顺序包含相同的元素（即相等的数组），则认为二者是相等的。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2022/06/01/ex1.jpg)

```
输入：grid = [[3,2,1],[1,7,6],[2,7,7]]
输出：1
解释：存在一对相等行列对：
- (第 2 行，第 1 列)：[2,7,7]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2022/06/01/ex2.jpg)

```
输入：grid = [[3,1,2,2],[1,4,4,5],[2,4,2,2],[2,4,2,2]]
输出：3
解释：存在三对相等行列对：
- (第 0 行，第 0 列)：[3,1,2,2]
- (第 2 行, 第 2 列)：[2,4,2,2]
- (第 3 行, 第 2 列)：[2,4,2,2]
```

 

**提示：**

- `n == grid.length == grid[i].length`
- `1 <= n <= 200`
- `1 <= grid[i][j] <= 10^5`



#### 分析

模拟题，遍历每一行，排查每一列如果行与列相等，结果加1。



#### 代码

```java
class Solution {
    public int equalPairs(int[][] grid) {
        int n = grid.length;
        int res = 0;
        // 遍历每一行
        for (int i = 0; i < n; i++) {
            int[] arr = grid[i];
            // 遍历每一列，判断行与列是否完全相等
            for (int j = 0; j < n; j++) {
                if (equals(arr, grid, j)) res++;
            }
        }

        return res;
    }

    private boolean equals(int[] arr, int[][] grid, int col) {
        for (int row = 0; row < grid.length; row++) {
            if (arr[row] != grid[row][col]) return false;
        }
        return true;
    }
}
```

------

### 题目三、[6126. 设计食物评分系统](https://leetcode.cn/problems/design-a-food-rating-system/)【中等】

设计一个支持下述操作的食物评分系统：

- **修改** 系统中列出的某种食物的评分。
- 返回系统中某一类烹饪方式下评分最高的食物。

实现 `FoodRatings` 类：

- ```
  FoodRatings(String[] foods, String[] cuisines, int[] ratings)初始化系统。食物由foods、cuisines和ratings描述，长度均为n。
  ```

  - `foods[i]` 是第 `i` 种食物的名字。
  - `cuisines[i]` 是第 `i` 种食物的烹饪方式。
  - `ratings[i]` 是第 `i` 种食物的最初评分。

- `void changeRating(String food, int newRating)` 修改名字为 `food` 的食物的评分。

- `String highestRated(String cuisine)` 返回指定烹饪方式 `cuisine` 下评分最高的食物的名字。如果存在并列，返回 **字典序较小** 的名字。

注意，字符串 `x` 的字典序比字符串 `y` 更小的前提是：`x` 在字典中出现的位置在 `y` 之前，也就是说，要么 `x` 是 `y` 的前缀，或者在满足 `x[i] != y[i]` 的第一个位置 `i` 处，`x[i]` 在字母表中出现的位置在 `y[i]` 之前。

 

**示例：**

```
输入
["FoodRatings", "highestRated", "highestRated", "changeRating", "highestRated", "changeRating", "highestRated"]
[[["kimchi", "miso", "sushi", "moussaka", "ramen", "bulgogi"], ["korean", "japanese", "japanese", "greek", "japanese", "korean"], [9, 12, 8, 15, 14, 7]], ["korean"], ["japanese"], ["sushi", 16], ["japanese"], ["ramen", 16], ["japanese"]]
输出
[null, "kimchi", "ramen", null, "sushi", null, "ramen"]

解释
FoodRatings foodRatings = new FoodRatings(["kimchi", "miso", "sushi", "moussaka", "ramen", "bulgogi"], ["korean", "japanese", "japanese", "greek", "japanese", "korean"], [9, 12, 8, 15, 14, 7]);
foodRatings.highestRated("korean"); // 返回 "kimchi"
                                    // "kimchi" 是分数最高的韩式料理，评分为 9 。
foodRatings.highestRated("japanese"); // 返回 "ramen"
                                      // "ramen" 是分数最高的日式料理，评分为 14 。
foodRatings.changeRating("sushi", 16); // "sushi" 现在评分变更为 16 。
foodRatings.highestRated("japanese"); // 返回 "sushi"
                                      // "sushi" 是分数最高的日式料理，评分为 16 。
foodRatings.changeRating("ramen", 16); // "ramen" 现在评分变更为 16 。
foodRatings.highestRated("japanese"); // 返回 "ramen"
                                      // "sushi" 和 "ramen" 的评分都是 16 。
                                      // 但是，"ramen" 的字典序比 "sushi" 更小。
```

 

**提示：**

- `1 <= n <= 2 * 10^4`
- `n == foods.length == cuisines.length == ratings.length`
- `1 <= foods[i].length, cuisines[i].length <= 10`
- `foods[i]`、`cuisines[i]` 由小写英文字母组成
- `1 <= ratings[i] <= 10^8`
- `foods` 中的所有字符串 **互不相同**
- 在对 `changeRating` 的所有调用中，`food` 是系统中食物的名字。
- 在对 `highestRated` 的所有调用中，`cuisine` 是系统中 **至少一种** 食物的烹饪方式。
- 最多调用 `changeRating` 和 `highestRated` **总计** `2 * 10^4` 次



#### 分析

设计题，按照题意设计即可。

1.返回烹饪方式下评分最高的食物：所以需要用一个排序的数据结构，可以用TreeSet和PriorityQueue，又因为需要常数时间复杂度的更新操作，所以使用TreeSet，需要使用一个Map存放key为cuisine，value为TreeSet。

2.根据food更新rating：要找到对应的food，然后从TreeSet中移除之前的food，放入新的food，所以需要使用一个Map存放food，key为foodName，value为Food。



关于第二个Map是否需要，如果是普通的Set只要通过foodName重写equals和hashCode，foodName相同时会替换原先的food，但是TreeSet不行，由于TreeSet指定rating和foodName进行排序，所以不能只通过foodName进行替换，这里WA了一次。

#### 代码

```java
public class FoodRatings {
    Map<String, TreeSet<Food>> cuisineMap = new HashMap<>();

    Map<String, Food> foodMap = new HashMap<>();

    public FoodRatings(String[] foods, String[] cuisines, int[] ratings) {
        int n = foods.length;
        for (int i = 0; i < n; i++) {
            String foodName = foods[i], cuisine = cuisines[i];
            int rating = ratings[i];
            Food food = new Food(foodName, rating, cuisine);
            foodMap.put(foodName, food);

            TreeSet<Food> foodSet = cuisineMap.getOrDefault(cuisine, new TreeSet<>((f1, f2) -> {
                if (f1.rating == f2.rating) {
                    return f1.food.compareTo(f2.food);
                }

                return f2.rating - f1.rating;
            }));
            foodSet.add(food);
            cuisineMap.put(cuisine, foodSet);
        }
    }

    public void changeRating(String foodName, int newRating) {
        Food preFood = foodMap.get(foodName);
        String cuisine = preFood.cuisine;
        Food food = new Food(foodName, newRating, cuisine);
        foodMap.put(foodName, food);

        TreeSet<Food> foodSet = cuisineMap.get(cuisine);
        foodSet.remove(preFood);
        foodSet.add(food);
        cuisineMap.put(cuisine, foodSet);
    }

    public String highestRated(String cuisine) {
        return cuisineMap.get(cuisine).first().food;
    }

    private static class Food {
        String food;

        int rating;

        String cuisine;

        public Food(String food, int rating, String cuisine) {
            this.food = food;
            this.rating = rating;
            this.cuisine = cuisine;
        }
    }
}
```

------

### 题目四、[6127. 优质数对的数目](https://leetcode.cn/problems/number-of-excellent-pairs/)【困难】

给你一个下标从 **0** 开始的正整数数组 `nums` 和一个正整数 `k` 。

如果满足下述条件，则数对 `(num1, num2)` 是 **优质数对** ：

- `num1` 和 `num2` **都** 在数组 `nums` 中存在。
- `num1 OR num2` 和 `num1 AND num2` 的二进制表示中值为 **1** 的位数之和大于等于 `k` ，其中 `OR` 是按位 **或** 操作，而 `AND` 是按位 **与** 操作。

返回 **不同** 优质数对的数目。

如果 `a != c` 或者 `b != d` ，则认为 `(a, b)` 和 `(c, d)` 是不同的两个数对。例如，`(1, 2)` 和 `(2, 1)` 不同。

**注意：**如果 `num1` 在数组中至少出现 **一次** ，则满足 `num1 == num2` 的数对 `(num1, num2)` 也可以是优质数对。

 

**示例 1：**

```
输入：nums = [1,2,3,1], k = 3
输出：5
解释：有如下几个优质数对：
- (3, 3)：(3 AND 3) 和 (3 OR 3) 的二进制表示都等于 (11) 。值为 1 的位数和等于 2 + 2 = 4 ，大于等于 k = 3 。
- (2, 3) 和 (3, 2)： (2 AND 3) 的二进制表示等于 (10) ，(2 OR 3) 的二进制表示等于 (11) 。值为 1 的位数和等于 1 + 2 = 3 。
- (1, 3) 和 (3, 1)： (1 AND 3) 的二进制表示等于 (01) ，(1 OR 3) 的二进制表示等于 (11) 。值为 1 的位数和等于 1 + 2 = 3 。
所以优质数对的数目是 5 。
```

**示例 2：**

```
输入：nums = [5,1,1], k = 10
输出：0
解释：该数组中不存在优质数对。
```

 

**提示：**

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^9`
- `1 <= k <= 60`



#### 分析

`num1 OR num2` 和 `num1 AND num2` 的二进制表示中值为 **1** 的位数之和：

`num1 AND num2` 中1的个数：num1和num2中二进制都为1的个数

`num1 OR num2` 中1的个数：num1二进制1的个数与num2二进制1的个数之和 - num1和num2中二进制都为1的个数

所以`num1 OR num2` 和 `num1 AND num2` 的二进制表示中值为 **1** 的位数之和为num1二进制1的个数与num2二进制1的个数之和 。



1.给定一个数num1，计算出num1二进制中1的个数

2.优质数对的num2需要满足num1中1的个数与num2中1的个数之和大于等于k。



#### 代码

```java
lass Solution {
    public long countExcellentPairs(int[] nums, int k) {
        int[] arr = new int[30];
        Set<Integer> set = new HashSet<>();

        for (int num : nums) set.add(num);
        for (int num : set) {
            int count = get(num);
            arr[count]++;
        }

        long res = 0;
        for (int num : set) {
            int count = get(num);
            int start = Math.max(k - count, 0);
            // 这里可以使用前缀和进行优化，减小时间复杂度
            for (int i = start; i < arr.length; i++) {
                res += arr[i];
            }
        }

        return res;
    }

    private static int get(int p) {
        int res = 0;
        while (p > 0) {
            if ((p & 1) == 1) res++;
            p >>= 1;
        }
        return res;
    }
}
```





