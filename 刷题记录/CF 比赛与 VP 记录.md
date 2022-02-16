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

令 $[x,y]$ 值域内的数为 $1$，其余为 $-1$，则要求划分恰好 $k$ 段和 $>1$ 的段。

贪心地，从左往右每次取最小的和 $=1$ 的段。可以把 $[x,y]$ 合法的条件转化为整个序列的和 $\ge k$。

那么可以双指针，$\mathcal O(n)$。

### C. Paint the Middle

每个权值的位置集合，只有左端点和右端点有用，记为一个“区间”。

如果一个区间被另一个区间包含，也是无用的。最后一定会形成若干左、右端点都递增的区间。

最优策略是：对于当前区间 $[l_i,r_i]$，找到最大的 $j$ 满足 $l_j\in [l_i,r_i]$，操作 $j$ 解决掉 $i+1\dots j-1$ 区间的右端点，和递归解决 $j$ 后面的区间；然后操作 $i$。这样的过程每次会遗漏一个。

### \*D. Flipping Range

取 $B$ 集合的 $\gcd=g$，$B$ 集合能够表示的所有数，都是 $g$ 的倍数（辗转相除来得到 $\gcd$）。等价于每次操作 $g$。

记是否取负的操作序列为 $s$，每次将 $s$ 序列中一段长为 $g$ 的区间取反。可以发现设 $f_x=\bigoplus_{i\bmod g=x}s_i$，所有 $f_x$ 是相等的。

我们声称所有 $f_x$ 是相等的 $s$ 序列一定可以通过合法操作得到。证明就是把这样的 $s$ 还原为全 $0$，从左往右每操作一次消去一个 $1$，最后 $g-1$ 个位置一定都是 $0$。

那么可以下标按 $\bmod g$ 分类进行 DP，$\mathcal O(n)$。

## Codeforces Global Round 19

[link](https://codeforces.com/contest/1637)

### B. MEX and Array

可以暴力 $\mathcal O(n^4)$ DP。观察到最优策略一定是每个数分一段，那么考虑每个数的贡献可以做到 $\mathcal O(n)$。

### C. Andrew and Stones

存在奇数的话，如果有大于 $1$ 个奇数并且不都为 $1$ 的话，可以奇数直接相互操作变为偶数。

### D. Yet Another Minimization Problem

拆开平方，操作能够影响的部分是 $a_i\sum_{j<i}a_j$ 和 $b_i\sum_{j<i}b_j$，DP 记录操作后 $a_i$ 的前缀和即可，$\mathcal O(n^2V)$。

### \*E. Best Pair

由于不同数的种类数是 $\mathcal O(\sqrt n)$ 的，枚举 $\mathrm{cnt}_x,\mathrm{cnt}_y$ 元素。

按 $\mathrm{cnt}$ 分类后，枚举 $\mathrm{cnt}_x$ 集合的所有元素，再**从大到小**枚举 $\mathrm{cnt}_y$ 集合的元素，用 $\texttt{std::set<>}$ 跳过禁止点对。对于每个 $x$，查找到第一个未被禁止的 $y$ 即可退出。就可以做到 $\mathcal O(n\log m+m\log m)$。

### \*F. Towers

容易发现 towers 一定建在叶子上。

取 $h_i$ 最大的点作为根，有两个叶子的 $e$ 值会 $\ge \max h_i$，那么每个点只需要考虑下方一侧的限制。可以树上贪心，每个点增加子树内最大的叶子。

### \*G. Birthday

可以组合出来的操作是：$(0,x)\to(x,x)\to(0,2x)$。

考虑把所有数变为 $2$ 的幂，然后统一。

取 $n$ 以内最大的 $k=2^t$，操作 $(k-i,k+i)$ 可以得到 $(2k,2i)$。然后会剩下一段 $\{1,2,3,\dots k-(n-k)-1\}$ 和一段 $\{2,4,6,\dots 2(n-k)\}$，变为递归的子问题。

这样分治的操作次数是 $\mathcal T(n)=2\mathcal T(\frac n2)+\mathcal O(n)=\mathcal O(n\log n)$ 的。

### \*H. Minimize Inversions Number

设 $d_i$ 表示只将 $i$ 移动至开头时，逆序对的变化量。若选取的子序列下标集合为 $q$，则排列 $p$ 的逆序对数变为
$$
\mathrm{inv}(p)+\sum_{j\in q}d_j+\mathrm{inv}(q)-\mathrm{sqt}(q),
$$
其中 $\mathrm{inv}(p),\mathrm{sqt}(p)$ 分别表示 $p$ 的逆序对、顺序对数。化简一下，本题需要最小化的是
$$
\sum_{i\in q}d_i+2\cdot \mathrm{inv}(q).
$$
然后有结论：对于 $q$ 集合中元素 $i$，若存在 $j$ 满足 $i<j,p_i>p_j$，则 $j\in q$。

> 证明：
>
> 反证 + 调整。假设该结论不正确，取 $q$ 集合中 $|i-j|$ **最小**的一对 $(i,j)$ 满足 $i<j,p_i>p_j$ 并且 $i$ 选取而 $j$ 未选取。
>
> 考虑调整为 $i$ 不选取而 $j$ 选取，分类讨论各部分对答案变化量的贡献，有
>
> ![](https://s4.ax1x.com/2022/02/16/HW66fJ.png)
>
> 由于 $(i,j)$ 的最小性，红线划去部分不会出现，则答案一定不会变劣。
>
> 每次调整后选取的子序列的下标之和增加，调整法将在有限步内结束。

此时问题转化为最小化，
$$
\sum_{i\in q}d_i+2\left(\sum_{i\in q}\sum_{j>i}[q_j<q_i]\right).
$$
可以 $\mathcal O(n\log n)$ 预处理，然后贪心解决。
