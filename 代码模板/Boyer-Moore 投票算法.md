### Boyer-Moore 投票算法

Boyer-Moore 投票算法（Boyer-Moore Majority Vote Algorithm）是一种线性时间复杂度、常数空间复杂度的算法，用于在数组中找到 **多数元素**（即出现次数超过一半的元素）。

#### 算法思想
Boyer-Moore 投票算法的核心思想是“抵消法”。假设数组中存在多数元素，它的出现次数超过一半，那么通过成对抵消不同的元素，最后剩下的元素必然是多数元素。

#### 算法步骤
1. **初始化**：选定一个候选元素 `candidate`，并设置计数器 `count` 初始值为 0。
2. **遍历数组**：
   - 如果当前计数 `count` 为 0，更新候选元素 `candidate` 为当前元素，并将 `count` 设置为 1。
   - 如果当前元素等于 `candidate`，则计数器 `count` 加 1。
   - 如果当前元素不等于 `candidate`，则计数器 `count` 减 1。
3. **输出结果**：在一次遍历结束后，`candidate` 即为可能的多数元素。为了确保 `candidate` 是多数元素，可以再进行一次遍历，验证它的出现次数是否超过数组长度的一半。

#### 代码实现

```cpp
#include <iostream>
#include <vector>

int majorityElement(const std::vector<int>& nums) {
    int candidate = 0;
    int count = 0;

    // 第一次遍历，找到候选元素
    for (int num : nums) {
        if (count == 0) {
            candidate = num;  // 更新候选元素
        }
        count += (num == candidate) ? 1 : -1;
    }

    // 第二次遍历，验证候选元素是否为多数元素
    count = 0;
    for (int num : nums) {
        if (num == candidate) {
            count++;
        }
    }

    if (count > nums.size() / 2) {
        return candidate;  // 返回多数元素
    }

    return -1;  // 如果不存在多数元素，返回 -1
}

int main() {
    std::vector<int> nums = {2, 2, 1, 1, 1, 2, 2};
    int result = majorityElement(nums);
    if (result != -1) {
        std::cout << "多数元素是: " << result << std::endl;
    } else {
        std::cout << "不存在多数元素" << std::endl;
    }
    return 0;
}
```

#### 解释
1. **第一次遍历**：
   - 我们通过抵消不同的元素，将数组中的不同元素相互抵消，最终剩下的 `candidate` 是可能的多数元素。
   
2. **第二次遍历**：
   - 验证 `candidate` 是否确实是多数元素，即检查 `candidate` 的出现次数是否大于数组长度的一半。如果满足条件，则返回该元素，否则返回 `-1`。

#### 时间复杂度和空间复杂度
- **时间复杂度**：O(n)，只需要两次遍历数组。
- **空间复杂度**：O(1)，只使用了几个额外的变量，不需要额外的存储空间。

#### 适用范围
Boyer-Moore 投票算法适用于找到出现次数 **超过一半** 的元素。如果数组中不存在这样的元素，算法的第二次遍历会确保返回 `-1`。如果数组中可能存在多个重复元素但没有绝对多数，这个算法不适用。