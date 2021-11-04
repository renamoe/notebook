## ARC103D - Robot Arms

[link](https://atcoder.jp/contests/arc103/tasks/arc103_b)

有解的条件是 $x+y$ 奇偶性相同，为 $\sum d_i$ 的奇偶性。

根据 $m$ 的限制应该想到二进制拆分。

$1,2,4\dots$ 能够覆盖的范围，再网格图上表示为一层层菱形。根据奇偶性可能需要加一个 $1$ 偏移一下。构造方式就是 $d_i$ 从大到小每次选择距离绝对值较大的移位移动，能够覆盖所有可到达的点。

[submission(3)](https://atcoder.jp/contests/arc103/submissions/27017414)

