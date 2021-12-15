## UOJ#105. 【APIO2014】Beads and wires

[link](https://uoj.ac/problem/105)

一条蓝线连接连续三个点，直接 DP 发现并不对，反例：

![](https://s4.ax1x.com/2021/12/16/T9FpdO.png)

但是根据生成的过程，如果确定一个根，所有蓝线一定是 $u-\mathrm{fa}(u)-\mathrm{fa}(\mathrm{fa}(u))$ 的形态。

DP 设 $f(u,0/1)$ 表示 $u$ 是否为蓝线中点的最大价值。$f(u,1)$ 中某个儿子的贡献是不一样的，而且是最大值，换根 DP 时如果该儿子 $v$ 是最大值，那么去掉 $v$ 的贡献后应该由次大值顶替。

[submission(2)](https://uoj.ac/submission/520805)

