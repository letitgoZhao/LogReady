# 50. Pow(x, n)


> [题目链接](https://leetcode.cn/problems/powx-n/description/?envType=study-plan-v2&envId=top-interview-150)


## 快速幂方法
当我们要计算 $x^n$时，我们可以先递归地计算出$y=x^⌊n/2⌋$, 其中 ⌊a⌋ 表示对 a 进行下取整；

- 根据递归计算的结果，如果`n`为偶数，那么 $x^n=y^2$; 如果`n`为奇数，那么$x^n=y^2x$。
- 递归的边界为`n=0`，`任意数的 0 次方均为 1`。
- 由于每次递归都会使得指数减少一半，因此递归的层数为 O(logn)，算法可以在很快的时间内得到结果。

```cpp
class Solution {
public:
    double myPow(double x, int n) {
        double ans = quickMul(x, n);
        return (n >= 0) ? ans : 1.0 / ans;
    }
    double quickMul(double x, int N) {
        // 核心思想
        // x=64, 偶数, 64 -> 32 -> 16 -> 8 -> 4 -> 2 -> 1 -> 0
        // x=77, 奇数, 77 -> 38 -> 19 -> 9 -> 4 -> 2 -> 1 -> 0
        // x^n -> y = x^[n/2]
        // 1. 如果n为偶数, x^n = y * y
        // 2. 如果n为基数, x^n = y * y * x
        if (N == 0)
            return 1.0L;
        double y = quickMul(x, N / 2);
        return (N % 2 == 0) ? y * y : y * y * x;
    }
};
```