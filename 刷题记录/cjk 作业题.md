## LOJ#3157. 「NOI2019」机器人

[link](https://loj.ac/p/3157)

枚举最大值的位置（如果有多个，选最右侧的），分成两个长度差不超过 $2$ 的区间递归考虑。有 DP

$$
f(l,r,k)=\sum_{|(r-i)-(i-l)|\le 2}\left(\sum_{x\le k}f(l,i-1,x)\right)\left(\sum_{y< k}f(i+1,r,y)\right)
$$

我们知道 $f(l,r,k)$ 为关于 $k$ 的多项式。大量的前缀和操作，考虑使用下降幂多项式表示。

下降幂多项式的差分：

$$
(x+1)^{\underline i}-x^{\underline i}=ix^{\underline{i-1}}
$$

前缀和：

$$
\sum_{x=0}^{n-1}x^{\underline i}=\sum_{x=0}^{n-1}\frac{(x+1)^{\underline{i+1}}-x^{\underline{i+1}}}{i+1}=\frac{n^{\underline{i+1}}}{i+1}
$$

$$
\sum_{i=0}^{x-1}\sum_{j=0}^{D}a_ji^{\underline j}=\sum_{j=0}^Da_j\frac{x^{\underline{j+1}}}{j+1}
$$

下降幂多项式可以 $\mathcal O(\text{项数})$ 的做前缀和。

下降幂多项式的乘法暴力做，$x^{\underline i}$ 乘 $(x-i)^{\underline j}$ 贡献到 $x^{\underline{i+j}}$，由 $x^{\underline i}=(x-1)^{\underline i}+i(x-1)^{\underline{i-1}}$ 展开，可以 $\mathcal O(n^2)$ 做乘法。

对于 $[l_i,r_i]$ 的限制，就是维护分段函数，具体见代码。

复杂度 $\mathcal O(n\sum \mathrm{len}^2)$，跑的飞快。

[submission(0)](https://loj.ac/s/1336139)

## LOJ#2087. 「NOI2016」国王饮水记

[link](https://loj.ac/p/2087)

首先有结论：

- 从小到大排序后，每次操作的一定是一个区间（调整）；
- 每个点至多会被操作一次；
- 操作的区间一定是最大的连续若干段；

那么有 DP $f(i,j)$ 表示操作 $i$ 次后最大点为 $j$ 的最大答案，

$$
f(i,j)\gets \frac{f(i-1,k)+s_j-s_k}{j-k+1}
$$

观察为斜率优化形式，

$$
f(i,j)=\frac{s_j-(s_k-f(i-1,k))}{j-(k-1)}
$$

单调队列维护下凸壳即可。

答案要求高精度小数，但是最优的转移只需要 $\texttt{double}$ 类型即可确定，记录转移路径，最后用高精度小数计算一遍。

$\mathcal O(n^2+np)$。

发现更新答案时 $\ge$ 写成 $>$ 一直过不去，原因应该是：由贪心可得，操作过程中，较小数区间操作，较大数为单个操作，每次转移的区间长度不会大于上一次转移的区间长度。DP 后面过程中过多长度为 $1$ 的区间影响精度，$\texttt{double}$ 类型的精度已经无法表示。操作次数更多更优，人为地取 $\min(k,n-1)$ 次即可。

[submission($+\infty$)](https://loj.ac/s/1337418)
