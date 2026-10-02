# V2EX 发帖 · 分享创造节点

## 标题
做了一个哥德巴赫猜想的数值研究，发现涨落是亚泊松的

## 正文（正文区）

大家好，分享一个业余做的数论数值研究项目——金翼计划。

### 一句话结论

哥德巴赫分拆数 g(N) 的涨落是**亚泊松**的（Fano 因子 F ≈ 0.30），比泊松分布安静约 3 倍。

之前文献里看到的"超泊松"是均值漂移造成的统计假象——在 10⁹ 尺度上，漂移占了总方差的 98%。

### 做了什么

- 算到了 10 亿（10⁹），17 个尺度的系统测量
- C++ 主路径（埃氏筛 + 逐偶数扫描 + OpenMP）+ Python/FFT 独立验证，双路误差 ≤ 10⁻⁶
- 三种独立方法（漂移修正、ANOVA 上界、窄窗口直接测量）一致指向亚泊松结论
- 窄窗口实验（窗口宽度仅 10%）模型无关地测得 κ = 0.620 < 1，亚泊松无条件成立

### 一些副产品

- 零参数漂移律：从 Hardy-Littlewood 奇异级数直接导出 K(N) 均值漂移，无拟合参数，10⁹ 处偏差 0.008%
- d(N) 对称距离统计：最大值大致服从 (log N)^γ 幂律，γ ≈ 3.5
- 七个开放问题，包括 κ 的极限常数、亚泊松机理等

### 为什么发 V2EX

因为觉得这里的程序员/技术人群可能会对"大规模数值计算 + 数学问题"这个组合感兴趣。
另外我们有个疑问：这个方向有没有人做过类似的数值实验？如果有知道相关文献的欢迎指个路。

### 链接

- 完整版报告（HTML，交互式图表）：https://luinstein.github.io/goldwing-research/paper/goldwing_v1.6_subpoisson.html
- 项目主页（有可视化）：https://luinstein.github.io/goldwing-research/
- GitHub 仓库：https://github.com/luinstein/goldwing-research
- 素数星空可视化：https://luinstein.github.io/goldwing-research/visualizations/prime_starry_sky.html

---

*金翼计划 · 耦合刚性研究*
