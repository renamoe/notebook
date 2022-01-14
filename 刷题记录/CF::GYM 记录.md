## gym103371J. Periodic Ruler

[link](https://codeforces.com/gym/103371/problem/J)

先排除不能作为周期的正整数，也就是所有不同数对的坐标之差的所有约数。

然后再找不能满足是最小正周期的正整数，这样的数 $k$ 一定是 $\le n$ 的。因为如果 $k> n$ 把其他所有点映射到 $[0,k)$ 中，至少有一个空位，可以放一个 unique 的数。

然后怎么暴力怎么来。

[submission(3)](https://codeforces.com/gym/103371/submission/142551700)


