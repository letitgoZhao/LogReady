# 魔法环加权求和

**问题描述:**

给你一个长度为 n 的环形数组 nums，你可以选择任意一个位置 k 作为起点将环形数组「断开」，得到一个线性数组 b，其中 b[i] = nums[(k + i) % n]。

对于断开后的线性数组 b，计算加权交替和：

$$
S = 1 \times b[0] - 2 \times b[1] + 3 \times b[2] + \cdots + (-1)^{n-1} \times n \times b[n-1]
$$

请你返回所有可能断开位置中，加权交替和 S 的最大值。给你一个环形数组 nums，请返回加权交替和的最大值。

数据范围: `1 <= n <= 1000`, `-1000 <= nums[i] <= 1000`。

**代码示例如下所示:**

```python
class Solution:
    def maxMagicSum(self, nums: List[int]) -> int:
        n = len(nums)
        # 用于记录最大加权和
        max_sum = float('-inf')  
        
        # 对每个可能的起始位置 k 进行计算
        for k in range(n):
            current_sum = 0
            # 计算从位置 k 开始的加权交替和 S
            for i in range(n):
                sign = 1 if i % 2 == 0 else -1  # 加权符号，根据 i 的奇偶决定
                current_sum += sign * (i + 1) * nums[(k + i) % n]  # 计算每个位置的贡献
            # 更新最大加权交替和
            max_sum = max(max_sum, current_sum)
        
        return max_sum
```