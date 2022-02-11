## CF663C. Binary Table

[link](https://codeforces.com/contest/662/problem/C)

暴力做法是枚举行的翻转情况，那么每一列是否翻转更优就确定了，也就是

$$
\min_x\{\sum_{i}^mf_{a_i\oplus x}\}.
$$

换一种表示方式，设 $c_i$ 表示值为 $i$ 的数个数，

$$
\min_x\{\sum_ic_i\times f_{i\oplus x}\}
$$

可以发现是异或卷积。

[submission(0)](https://codeforces.com/contest/662/submission/145626071)

## AGC016F. Games on DAG

[link](https://atcoder.jp/contests/agc016/tasks/agc016_f)

两个棋子独立，转化为求多少种删边方案使得 $\mathrm{SG}(1)\oplus\mathrm{SG}(2)=0$。

状压 DP 设 $f(S)$ 表示 $S$ 集合的答案。

DAG 的点是按 SG 值分层的。设 $S$ 集合的子集 $T$ 表示 $\mathrm{SG}$ 值 $> 0$ 的点集，将 $S\setminus T$ 删去，$T$ 集合 $\mathrm{SG}$ 值整体减一，转化为递归的子问题。

$T$ 集合需要满足：

- $T$ 中每个元素都至少有一条边指向 $S\setminus T$；
- $S\setminus T$ 内部不允许有边；
- $S\setminus T$ 指向 $T$ 集合的边随意。

如果 $S$ 集合不包含 $1,2$，那么内部的边任意。

复杂度 $\mathcal O(3^nn)$。

[submission(0)](https://atcoder.jp/contests/agc016/submissions/29185134)

## CF1530F. Bingo

[link](https://codeforces.com/contest/1530/problem/F)

先容斥对角线，强制选 $1$ 的将概率改为 $1$。然后枚举行的子集容斥，剩下的列就是要求每列至少有一个 $0$，记录全 $1$ 概率补集转化一下。复杂度 $\mathcal O(2^{n+2}n)$。

[submission(0)](https://codeforces.com/contest/1530/submission/145806869)

## CF1523F. Favorite Game

[link](https://codeforces.com/contest/1523/problem/F)

正确的策略一定是形如：`tower -> task -> task -> tower -> tower -> task ...`

状压已经得到的 tower 集合，用一些交换 key 和 value 的技巧，可以得到如下状态：

- $f(S,i)$ 表示已得到 $S$ 集合的 tower，完成了 $i$ 个 task 的最少时间；
- $g(S,i)$ 表示已得到 $S$ 集合的 tower，当前在第 $i$ 个 task，最多完成了的 task 数量。

预处理一些距离，然后可以按状态中 $S,i$ 的变化关系进行转移。$\mathcal O(2^nm^2)$。

[submission(2)](https://codeforces.com/contest/1523/submission/145855003)

## CF1519F. Chests and Keys

[link](https://codeforces.com/contest/1519/problem/F)

如果确定了上锁的方案，Bob 的最少代价可以建最小割模型求解，Bob 的收益就是 $\sum_ia_i-\mathrm{mincost}$。

由于 $\mathrm{mincost}\le \sum_ia_i$，Alice 赢当且仅当最大流满流。

考虑状压左侧所有边的流量，类似轮廓线 DP，记录 $f(i,j,S,r)$ 表示到右侧第 $i$ 个点，左侧第 $j$ 个点，左侧流量剩余状态 $S$，右侧第 $i$ 条边剩余流量 $r$，Alice 加边的最小代价。

[submission(0)](https://codeforces.com/contest/1519/submission/145901219)

## LOJ#154. 集合划分计数

[link](https://loj.ac/p/154)

给出多项式 $F$ 和集合幂级数 $G$，求

$$
[x^{U}]\sum_{i=0}^nf_i\frac{G^i}{i!}.
$$

也就是多项式复合集合幂级数模板，参照 EI 论文。

![](https://s4.ax1x.com/2022/02/11/HasUY9.png)

[submission(0)](https://loj.ac/s/1378180)

## AGC043C. Giant Graph

[link](https://atcoder.jp/contests/agc043/tasks/agc043_c)

权值是 $10^{18}$ 的幂，一定是 $i+j+k$ 从大到小贪心选。

所有边按小到大定向，一个点能选当且仅当其出边都未选。对应 DAG 上博弈的 SG 值为 $0$。

可以看作三张图上三个棋子进行游戏，相互独立，则求

$$
\sum_{\mathrm{SG}(i)\oplus\mathrm{SG}(j)\oplus\mathrm{SG}(k)=0}K^{i+j+k}.
$$

FWT 进行异或卷积。

[submission(0)](https://atcoder.jp/contests/agc043/submissions/29217461)

## LOJ#2340. 「WC2018」州区划分

[link](https://loj.ac/p/2340)

部分分：

- $p=0$ 时就是求 $1+F+F^2+\dots$，复合或者求逆；
- $p=1$ 时有结论：$\sum_{\text{排列 }p}\prod_i\frac{a_{p_i}}{\sum_{j=0}^ia_{p_j}}=1$，所以就是 $\exp(F)$。

正解：

考虑子集 DP，

$$
f_S=\sum_{T\subseteq S}f_{S\setminus T}\cdot \frac{w_{T}^p}{w_S^p},
$$

把 $w_S^p$ 提出来，就是半在线的子集卷积。

子集卷积将子集大小放在第一维，按大小从小到大转移。$\mathcal O(2^nn^2)$。

[submission(2)](https://loj.ac/s/1378382)

## AGC024F. Simple Subsequence Problem

[link](https://atcoder.jp/contests/agc024/tasks/agc024_f)

设一个状态 $(S,T)$ 表示对应在某一个串上匹配时，当前匹配成功了 $S$，剩余部分为 $T$。所有串的所以状态放在一起，构成一个自动机。

枚举 $S$ 下一个填 $0/1$，在 $T$ 上贪心匹配；或者直接结束，转移到 $(S,\varnothing)$。

由于 $|S|+|T|$ 是 $\mathcal O(n)$ 的，记录分界点，可以做到 $\mathcal O(2^nn)$ DP。

[submission(1)](https://atcoder.jp/contests/agc024/submissions/29222140)
