## UOJ#692. 【UR #23】民意调查

[link](https://uoj.ac/problem/692)

枚举中位数和集合大小，然后左右两边就是背包。

处理前缀、后缀的背包，可以做到 $\mathcal O(n^3V)$。

从小到大枚举中位数，每次前缀插入、后缀删除，空间可以 $\mathcal O(n^2V)$。

[submission(0)](https://uoj.ac/submission/534688)

## CF1342F. Make It Ascending

[link](https://codeforces.com/contest/1342/problem/F)

每次枚举一个子集，加在其中一个点上。贪心地尽量靠前。

状态为 $f(S,i,j)$ 表示 $S$ 集合已选，分成了 $i$ 个子集，最后一个子集集中到了 $j$ 点，$a'_j$ 最小是多少。$\mathcal O(3^nn^2)$。

输出方案一定要仔细一点！

[submission(7)](https://codeforces.com/contest/1342/problem/F)

## CF1149D. Abandoning Roads

[link](https://codeforces.com/contest/1149/problem/D)

考虑做 Kruskal 的过程。

所有 $a$ 边构成的图，是若干连通块。每个连通块内的任意两点一定只能通过 $a$ 边连接。加入 $b$ 边后，任意两点的路径中，每个连通块至多经过一次。

状压所有连通块是否经过，可以得到 $\mathcal O(2^nm)$ 的 DP。转移顺序不确定，Dijkstra 或者用两个队列 BFS 来做。

对于一个大小不超过 $3$ 个点的连通块，任意两点距离不超过 $2a$，而离开该连通块再返回的路径长度 $>2b$，是一定不优的。所以不需要记录，复杂度降至 $\mathcal O(2^{n/4}m)$。

[submission(5)](https://codeforces.com/contest/1149/submission/146017788)

## CF1129D. Isolation

[link](https://codeforces.com/contest/1129/problem/D)

扫描线，从小到大枚举 $i$，给 $(\mathrm{last}(\mathrm{last}(i)),\mathrm{last}(i)]$ $-1$，$(\mathrm{last}(i),i]$ $+1$。

每次转移 $f_{i+1}$ 时就是求 $0\dots i$ 中满足 $c_j\le k$ 的 $f_j$ 之和。

分块，每个块维护一个桶。复杂度 $\mathcal O(n\sqrt n)$。

由于每个块内 $c_i$ 之差至多 $\mathcal O(\text{块长})$，所以空间是 $\mathcal O(n)$。原因考虑 $c$ 数组的差分中，每个位置只能是 $0$ 或 $1$。

[submission(0)](https://codeforces.com/contest/1129/submission/146040296)

## CF1039D. You Are Given a Tree

[link](https://codeforces.com/contest/1039/problem/D)

好像不是 DP。

对于一个确定的 $k$，可以在树上贪心计算答案，子树内如果能形成合法链就贪心匹配，否则将最长链传至父亲。

发现 $k$ 从小到大增长，答案变化的频率越来越慢。

根号分治，小于阈值 $S$ 的可以暴力做；大于 $S$ 的有 $\mathcal O(\frac nS)$ 段，可以二分得到每一段具体长度。

平衡一下可以做到 $\mathcal O(n\sqrt{n\log n})$。

较为卡常，树上 dfs 需要预处理 dfs 序进行模拟。

[submission(4)](https://codeforces.com/contest/1039/submission/146049086)


