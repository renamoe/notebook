CF 不打不行啊，赶紧回归老本行。

## Codeforces Round #767 (Div. 1)

[link](https://codeforces.com/contest/1628)

吐槽：我在做什么啊。

### A. Meximum Array 

处理每个权值的位置集合，然后每次贪心尽量让 $\mathrm{mex}$ 最大，其次尽量短。

### \*B. Peculiar Movie Preferences

经过一些枚举和贪心的讨论，只有形如 `1`, `2`, `3`, `22`, `33`, `23` 是有用的。

### \*C. Grid Xor

一行一行地满足。从第二行开始，如果当前格子上面的格子贡献是 $0$，那么操作一下当前格子。可以发现最后一定是填好的。

### \*D. Game on Sum

设 $f_{i,j}$ 表示剩余 $i$ 个数和 $j$ 个限制的答案。

假设此时 Alice 给出 $k$，Bob 操作后

$$
f_{i,j}=\min(f_{i-1,j}-k,f_{i-1,j-1}+k).
$$

为了最大化 $f_{i,j}$，Alice 会选择 $k=\frac{f_{i-1,j}+f_{i-1,j-1}}{2}$。

特别地 $f_{i,i}=i\cdot k$，据此可以 $\mathcal O(nm)$ DP。（Easy Version）

考虑每个 $f_{i,i}$ 的贡献，转化为网格图上每次向右或向右上走一步，$(i,i)\to (n,m)$ 的路径。第一步是不能向右上走的，所以路径方案数是 $\binom{n-i-1}{m-i}$。

可以 $\mathcal O(m)$ 求解。（Hard Version）

### \*E. Groceries in Meteor Town

首先建出 Kruskal 重构树，转化为每次查询 $x$ 和所有标记点的 LCA。

维护所有标记点的 LCA。一个点集的 LCA，就是 dfs 序最小点和最大点的 LCA。可以线段树维护。我的实现复杂度 $\mathcal O(m\log^2n)$。

## Codeforces Round #768 (Div. 1)

[link](https://codeforces.com/contest/1630)

### A. And Matching

当 $k=0$ 时，可以令 $i$ 和其补集 $n-1-i$ 配对。

$0< k< n-1$ 时可以调整一下，令 $k$ 所在 pair 和 $0$ 所在 pair 交换。

$k=n-1$ 时，$n=4$ 是无解的，$n>4$ 却可以调整，凑出 $n-2$ 再凑出 $1$。

### \*B. Range and Partition

### C. Paint the Middle

每个权值的位置集合，只有左端点和右端点有用，记为一个“区间”。

如果一个区间被另一个区间包含，也是无用的。最后一定会形成若干左、右端点都递增的区间。

最优策略是：对于当前区间 $[l_i,r_i]$，找到最大的 $j$ 满足 $l_j\in [l_i,r_i]$，操作 $j$ 解决掉 $i+1\dots j-1$ 区间的右端点，和递归解决 $j$ 后面的区间；然后操作 $i$。这样的过程每次会遗漏一个。


