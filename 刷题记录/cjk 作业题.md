## LOJ#3157. 「NOI2019」机器人

[link](https://loj.ac/p/3157)

枚举最大值的位置（如果有多个，选最右侧的），分成两个长度差不超过 $2$ 的区间递归考虑。有 DP

$$
f(l,r,k)=\sum_{|(r-i)-(i-l)|\le 2}\left(\sum_{x\le k}f(l,i-1,x)\right)\left(\sum_{y< k}f(i+1,r,y)\right)
$$

我们知道 $f(l,r,k)$ 为关于 $k$ 的多项式。大量的前缀和操作，考虑使用下降幂多项式表示，因为下降幂多项式可以 $\mathcal O(\text{项数})$ 的做积分（前缀和）。

下降幂多项式的乘法暴力做，$x^{\underline i}$ 乘 $(x-i)^{\underline j}$ 贡献到 $x^{\underline{i+j}}$，由 $x^{\underline i}=(x-1)^{\underline i}+i(x-1)^{\underline{i-1}}$ 展开，可以 $\mathcal O(n^2)$ 做乘法。

对于 $[l_i,r_i]$ 的限制，就是维护分段函数，具体见代码。

复杂度 $\mathcal O(n\sum \mathrm{len}^2)$，跑的飞快。

[submission(0)](https://loj.ac/s/1336139)

