1. #### all

all() 函数用于判断给定的可迭代参数 iterable 中的所有元素是否都为 TRUE，如果是返回 True，否则返回 False。

```python
# 示例列表
my_list = [True, True, False, True]

# 使用 all() 函数检查列表中的所有元素是否为真
result = all(my_list)

print(result)  # 输出: False
```



#### 2. bisect

`bisect` 是 Python 标准库中的一个模块，用于对有序序列进行二分查找。它提供了两个主要的函数 `bisect_left()` 和 `bisect_right()`，用于在有序序列中查找指定元素的插入位置，以保持序列的有序性。

```Python
import bisect

# 有序序列
sorted_list = [1, 3, 5, 7, 9]

# 在有序序列中查找元素 6 的插入位置
index = bisect.bisect_left(sorted_list, 6)

print(index)  # 输出: 3
```



#### 3.pairwise

迭代输入的序列，并返回相邻的元素对。

```Python
from itertools import pairwise

# 示例列表
numbers = [1, 2, 3, 4, 5]

# 使用 pairwise 生成相邻元素对
pairs = list(pairwise(numbers))

print(pairs)
```

输出

```
[(1, 2), (2, 3), (3, 4), (4, 5)]
```



#### 4.accumulate

`accumulate` 最常用于生成累积和，但也可以使用其他函数来生成累积结果。

```python
from itertools import accumulate

# 示例列表
numbers = [1, 2, 3, 4, 5]

# 计算累积和
accumulated_sums = list(accumulate(numbers))

print(accumulated_sums)
```

输出

```
[1, 3, 6, 10, 15]
```

