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

