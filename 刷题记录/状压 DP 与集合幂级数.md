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

