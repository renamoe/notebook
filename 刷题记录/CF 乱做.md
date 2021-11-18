## CF468D. Tree

[link](https://codeforces.com/contest/468/problem/D)

$$
\sum_{i=1}^n\mathrm{dis}(i,p_i)=\sum_{i=1}^n\mathrm{dis}(\mathrm{root},i)+\mathrm{dis}(\mathrm{root},p_i)-\mathrm{dis}(\mathrm{root},\mathrm{LCA}(i,p_i))
$$

也就是最小化 $\sum_i\mathrm{dis}(\mathrm{root},\mathrm{LCA}(i,p_i))$。

最好的情况当然是 $\mathrm{LCA}(i,p_i)=\mathrm{root}$，而以重心为 $\mathrm{root}$ 恰好能满足。因为任何一个子树大小不超过 $\lfloor\frac n2\rfloor$。

一个方便的构造方式是，在 dfs 序上每个点 $d_i$ 向 $d_{i+\lfloor\frac n2\rfloor}$ 配对，即可保证任意一对不在同一棵子树。

然后是保证字典序最小。从小到大依次满足，每次第 $i$ 个点找到子树外编号最小的点配对。

但是可能会出现某时刻不得不在同一子树内配对的情况。我们把每个点拆成入和出两个点，每个子树 $i$ 入点数 $f_i$，出点数 $g_i$，不合法的条件为存在子树 $g_i>\sum_{j\neq i} f_j$。

为了避免这种情况，当某一时刻存在某个子树 $i$ 满足 $g_i=\sum_{j\neq i} f_j$ 也就是 $f_i+g_i=\text{剩余入点数}$ 时，就一定要选 $i$ 子树。

我们用若干 $\texttt{std::set<>}$ 来实现，注意特殊讨论根。

[submission(1)](https://codeforces.com/contest/468/submission/128905288)

## CF264D. Colorful Stones

[link](https://codeforces.com/contest/264/problem/D)

这种二元组状态转移的问题可以放在网格图上，可以根据转移画出这样的图。

![](https://z3.ax1x.com/2021/09/24/4046ht.png)

可以猜测可到达的状态有这样一个大体的界，可以双指针 $\mathcal O(n)$ 计算。

界中也有若干不可到达的点，当且仅当 $\texttt{AB}$ 和 $\texttt{BA}$ 对应时产生，对每种可能的状态做前缀和即可。

[submission(1)](https://codeforces.com/contest/264/submission/129680644)


## CF1152F2. Neko Rules the Catniverse (Large Version)

[link](https://codeforces.com/contest/1152/problem/F2)

$k$ 很小，应该考虑按权值从小到大往序列里插入数，DP 状态记录序列的形态。

题目限制，相邻的数满足 $a_{i-1}+m\ge a_i$。当前要插入的是最大的数 $x$，那么 $x$ 能跟在 $y$ 后面一定要求 $x-y\le m$，否则只能插入到序列开头。

那么状压值域最后 $m$ 位的状态，DP 状态 $f(i,j,s)$ 表示值域 $1\dots i$ 当前序列已有 $j$ 个数，$i-m+1\dots i$ 的状态为 $S$。DP 很容易放到矩阵上，就可以 $\mathcal O((k2^m)^3\log n)$ 解决了。

[submission(0)](https://codeforces.com/contest/1152/submission/131374881)


## CF1043F. Make It One

[link](https://codeforces.com/problemset/problem/1043/F)

往集合里每加入一个数，$\gcd$ 质因子种类将会减小 $1$，否则这个数无用。

那么意味着答案至多为 $7$。先从小到大枚举答案 $k$，然后莫反计算 $f(d)$ 表示大小为 $k$ 的 $\gcd=d$ 的集合数量。

较为简单的莫反可以直接容斥，设 $\mathrm{cnt}(d)$ 表示 $d$ 的倍数的个数，

$$
f(d)={\mathrm{cnt}(d)\choose k}-\sum_{i\ge 2}f(i\cdot d)
$$

[submission(0)](https://codeforces.com/contest/1043/submission/131652274)


## CF1553H. XOR and Distance

[link](https://codeforces.com/contest/1553/problem/H)

考虑类似 FWT 的套路从低到高逐位满足。

记录 $f(d,x)$ 表示大于 $d$ 的位均与 $x$ 相同的所有数中，与 $x$ 异或后最小点对距离。转移就是 FWT 时合并两个无交的集合，需要维护 $f(d,x)$ 对应集合的 $\min,\max$。复杂度 $\mathcal O(k2^k)$。

[submission(0)](https://codeforces.com/contest/1553/submission/134263112)



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


## CF314E. Sereja and Squares

正解还真就是 $\mathcal O(n^2)$ 暴力 + 卡常，不适合口胡，[写了一发](https://codeforces.com/contest/314/submission/134666984)。

出题人脑子有问题。不过教训是要有梦想，适当对暴力卡常。

## CF1045H. Self-exploration

首先得到的性质是：$c_{00}+c_{01}+c_{10}+c_{11}+1$ 是合法串长度；$c_{10}$ 是 $0$ 的连通块数，$c_{01}+1$ 是 $1$ 的连通块数；并且 $c_{10}=c_{01}$ 或者 $c_{10}=c_{01}+1$，否则答案为 $0$。

不考虑限制，因为 $0,1$ 连通块相对顺序是确定的，方案数也就是 $\texttt{00}$ 分配到 $0$ 的若干连通块中、$\texttt{11}$ 分配到 $1$ 的若干连通块中的方案数，插板法即可。

对于限制，差分询问，枚举一个前缀相同然后容斥。细节很多，看代码。

[submission(5)](https://codeforces.com/contest/1045/submission/135519676)
