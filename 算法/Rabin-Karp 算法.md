### Rabin-Karp 算法简介

Rabin-Karp 是一种基于哈希值的字符串匹配算法，通常用于在大文本中搜索模式（子串）。与其他字符串匹配算法（如 KMP 算法）不同，Rabin-Karp 的核心思想是通过计算模式和文本子串的哈希值来加速比较操作，进而提高效率。

### 基本思想

1. **哈希函数**：首先，计算目标模式的哈希值，然后计算文本中与模式长度相等的每个子串的哈希值。
2. **哈希比较**：如果某个子串的哈希值与目标模式的哈希值相同，再进行字符逐个比较以确认是否完全匹配（避免哈希冲突）。
3. **滚动哈希**：通过滚动哈希的技巧，可以高效地从一个子串的哈希值快速得到下一个子串的哈希值，而无需重新计算所有字符的哈希。

Rabin-Karp 算法在最坏情况下的时间复杂度是 O(nm)，其中 `n` 是文本长度，`m` 是模式的长度。不过，在哈希函数表现良好的情况下，其期望时间复杂度为 O(n + m)。

### 算法步骤

1. **计算模式的哈希值**。
2. **计算文本中第一个子串的哈希值**。
3. **依次向右滑动窗口，使用滚动哈希技巧快速计算每个子串的哈希值，并与模式哈希值进行比较**。
4. **在哈希值相同时，进一步检查字符串是否完全匹配**。

### 滚动哈希公式

对于给定的模式和文本，假设使用的基数为 `P`，取模为 `MOD`，可以使用多项式哈希函数来计算哈希值：
$$
H(S[i:i+n]) = S[i] \cdot P^{n-1} + S[i+1] \cdot P^{n-2} + ... + S[i+n-1] \cdot P^0
$$
使用滚动哈希的技巧，可以在常数时间内计算下一个子串的哈希值：
$$
H(S[i+1:i+n+1])=(H(S[i:i+n])−S[i]⋅Pn−1)⋅P+S[i+n]H(S[i+1:i+n+1]) \\
= (H(S[i:i+n]) - S[i] \cdot P^{n-1}) \cdot P + S[i+n]H(S[i+1:i+n+1])\\
=(H(S[i:i+n])−S[i] \cdot P^{n-1})⋅P+S[i+n]
$$

### Rabin-Karp 算法的 C++ 实现

```cpp
#include <iostream>
#include <string>
#include <vector>

const int P = 31;  // 基数
const int MOD = 1e9 + 9;  // 取模常数，防止溢出

// 计算字符串的哈希值
long long computeHash(const std::string& s) {
    long long hash_value = 0;
    long long p_pow = 1;

    for (char c : s) {
        hash_value = (hash_value + (c - 'a' + 1) * p_pow) % MOD;
        p_pow = (p_pow * P) % MOD;
    }

    return hash_value;
}

// Rabin-Karp 算法实现
std::vector<int> rabinKarp(const std::string& text, const std::string& pattern) {
    int n = text.size();
    int m = pattern.size();
    
    long long pattern_hash = computeHash(pattern);
    long long current_hash = computeHash(text.substr(0, m));

    std::vector<int> occurrences;

    long long p_pow = 1;
    for (int i = 0; i < m; i++) {
        p_pow = (p_pow * P) % MOD;  // 计算 P^m，用于滚动哈希
    }

    // 滑动窗口逐个子串比较
    for (int i = 0; i <= n - m; i++) {
        if (current_hash == pattern_hash && text.substr(i, m) == pattern) {
            occurrences.push_back(i);  // 匹配成功
        }

        if (i < n - m) {
            current_hash = (current_hash - (text[i] - 'a' + 1) * p_pow % MOD + MOD) % MOD;  // 去掉前面字符
            current_hash = (current_hash * P + (text[i + m] - 'a' + 1)) % MOD;  // 加上新字符
        }
    }

    return occurrences;
}

int main() {
    std::string text = "abracadabra";
    std::string pattern = "abra";
    
    std::vector<int> occurrences = rabinKarp(text, pattern);

    std::cout << "Pattern found at indices: ";
    for (int i : occurrences) {
        std::cout << i << " ";
    }

    return 0;
}
```

### 代码说明

1. **哈希函数**：
   - 函数 `computeHash` 计算一个字符串的哈希值，使用多项式哈希方法，将每个字符的 ASCII 值乘以进制的对应幂。
2. **Rabin-Karp 算法**：
   - 函数 `rabinKarp` 实现了 Rabin-Karp 算法。首先计算模式的哈希值和文本中第一个子串的哈希值。然后通过滚动哈希逐步计算每个子串的哈希值，并与模式的哈希值进行比较。
   - 当哈希值相等时，通过 `substr` 进一步确认是否完全匹配。由于不同字符串可能有相同的哈希值，所以要做二次验证。
3. **滚动哈希**：
   - 使用滚动哈希更新每次的哈希值，减去旧字符的贡献，乘以基数 `P`，再加上新字符的贡献。
4. **匹配结果**：
   - 如果匹配成功，将模式第一次出现的位置加入结果列表。

### 算法复杂度

1. **时间复杂度**：
   - Rabin-Karp 算法的平均时间复杂度为 O(n + m)，其中 `n` 是文本长度，`m` 是模式长度。
   - 每次计算哈希值是常数时间，字符比较只在哈希值相等时进行（很少发生），因此平均性能优于暴力算法。
   - 在最坏情况下，所有子串的哈希值都可能与模式的哈希值相等，此时复杂度退化为 O(nm)，不过这很少发生。
2. **空间复杂度**：
   - 空间复杂度为 O(1)，因为只需要存储若干哈希值和常数个变量。

### 优点与缺点

#### 优点：

- 对大文本中查找模式非常高效，尤其是处理多个模式时，可以通过共享哈希函数来加速匹配。
- 算法实现简单，适用于模式匹配、重复子串检测等问题。

#### 缺点：

- **哈希冲突**：虽然哈希函数能将不同字符串映射到不同的哈希值，但存在少量哈希冲突的风险。为避免误匹配，需要在哈希值相等时再进行一次字符串的完全比较。
- **最坏情况时间复杂度**：在最坏情况下，Rabin-Karp 的时间复杂度可能会退化到 O(nm)。

### 应用场景

1. **多模式搜索**：由于哈希的计算是独立的，可以用于查找多个模式的场景。
2. **字符串重复检测**：通过计算不同子串的哈希值，可以快速检测重复的子串。
3. **基因序列匹配**：Rabin-Karp 可以用于 DNA 序列的匹配与比对问题。



LeetCode题目：

[1297. 子串的最大出现次数](https://leetcode.cn/problems/maximum-number-of-occurrences-of-a-substring/)

[1044. 最长重复子串](https://leetcode.cn/problems/longest-duplicate-substring/)：双重哈希解决哈希冲突

