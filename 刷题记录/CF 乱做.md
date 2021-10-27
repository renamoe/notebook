## CF1497E2. Square-free division (hard version)

[link](https://codeforces.com/problemset/problem/1497/E2)

首先 $a_i=\prod_i p_i^{c_i}$，其指数 $c_i$ 可以 $\bmod 2$，那么完全平方数的限制可以转化为相等的数对不超过 $k$ 对。

有状态 $f(i,j)$ 表示前 $i$ 个数修改 $j$ 次的最小分段数，那么可以做 $\mathcal O(n^2k)$ 的 DP。

转移时，贪心地，上一个转移点一定是尽量靠前更优。对于每个 $k$ 双指针处理每个 $i$ 的转移点。转移时只需要枚举当前段修改的次数，复杂度 $\mathcal O(nk^2)$。

[submission(2)](https://codeforces.com/contest/1497/submission/133150392)

## CF1527D. MEX Tree

[link](https://codeforces.com/contest/1527/problem/D)

考虑计算 $f_i$ 表示强制经过 $0\dots i$ 点的路径方案数，然后差分一下就是答案。

从小到达不断加点，维护最小路径的两端，知道无法形成一条路径。分类讨论一下，细节见代码。复杂度 $\mathcal O(n)$。

[submission(3)](https://codeforces.com/contest/1527/submission/133131181)