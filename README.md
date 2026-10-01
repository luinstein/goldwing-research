# 金翼计划 · Goldwing Research

> 十亿偶数里，素数对的涨落比泊松还安静。

金翼计划是一个关于哥德巴赫猜想的数值研究项目。我们通过大规模计算，系统测量了哥德巴赫分拆数的统计性质，发现了一些有趣的现象。

---

## 🌟 核心发现

### 1. 零参数漂移律 ✅

哥德巴赫归一化计数 \( K(N) = g(N) \cdot \ln^2 N / (N \cdot S(N)) \) 的均值可以从 Hardy–Littlewood 奇异级数**精确导出**，零拟合参数：

\[
\langle K(N) \rangle \approx 2C_2 \cdot \Phi\!\left(\frac{1}{\ln N}\right)
\]

在 \( N = 10^9 \) 处，理论预测与实测偏差仅 **0.008%**，且随尺度增大单调收窄。

### 2. 亚泊松涨落 ⭐

宽窗口下测得的 \( \kappa_{\text{naive}} > 1 \)（"超泊松"）是**均值漂移造成的假象**。扣除漂移后，真实涨落的 Fano 因子始终小于 1：

| 指标 | 值 | 含义 |
|------|-----|------|
| \( \kappa_{\text{noise}} \) | ~ 0.54 | 亚泊松 |
| Fano 因子 \( F \) | ~ 0.30 | 比泊松安静约 3 倍 |

### 3. 模型无关验证 🔬

通过**窄窗口实验**（窗口宽度仅 10%），在不依赖任何漂移模型的前提下直接测得：

\[
\kappa_{\text{naive}}^{\text{10%}} = 0.620 < 1
\]

由于漂移只会增大方差，\( \kappa_{\text{naive}} \geq \kappa_{\text{noise}} \) 恒成立。因此**亚泊松性质无条件成立**。

---

## 📂 仓库结构

```
goldwing-research/
├── README.md                    # 本文件
├── index.html                   # GitHub Pages 入口（重定向到报告）
├── paper/
│   └── goldwing_v1.6_subpoisson.html   # 研究报告（完整版）
├── visualizations/
│   ├── prime_starry_sky.html    # 素数星空（交互式可视化）
│   └── goldwing_constellation.html # 金翼星座（成果星空化）
├── data/
│   └── README.md                # 数据说明
└── docs/
    └── publication_plan_v1.html # 发布方案
```

---

## 📖 快速开始

### 阅读报告

直接打开 `paper/goldwing_v1.6_subpoisson.html`，或访问：
**[GitHub Pages](https://luinstein.github.io/goldwing-research/)**

### 浏览可视化

- **素数星空** — `visualizations/prime_starry_sky.html`
  乌拉姆螺旋、哥德巴赫彗星、素数星野，三种视角体验素数之美。
  [在线浏览](https://luinstein.github.io/goldwing-research/visualizations/prime_starry_sky.html)

- **金翼星座** — `visualizations/goldwing_constellation.html`
  把研究成果本身做成的星空页面，六大星座，七颗主星。
  [在线浏览](https://luinstein.github.io/goldwing-research/visualizations/goldwing_constellation.html)

---

## 📊 数据摘要

### 17 尺度测量（5×10⁵ 至 10⁹）

| N | ⟨K⟩ | κ_naive | κ_noise | 漂移占比 |
|---|-----|---------|---------|----------|
| 5×10⁵ | 0.72816 | 1.153 | 0.535 | 78.4% |
| 10⁶ | 0.72901 | 1.260 | 0.541 | 81.5% |
| 2×10⁶ | 0.72971 | 1.389 | 0.536 | 85.1% |
| 5×10⁶ | 0.73037 | 1.596 | 0.530 | 89.0% |
| 10⁷ | 0.73077 | 1.776 | 0.545 | 90.6% |
| 2×10⁷ | 0.73111 | 1.990 | 0.542 | 92.6% |
| 5×10⁷ | 0.73147 | 2.296 | 0.544 | 94.4% |
| 10⁸ | 0.73169 | 2.566 | 0.538 | 95.6% |
| 2×10⁸ | 0.73185 | 2.902 | 0.539 | 96.5% |
| 5×10⁸ | 0.73200 | 3.368 | 0.529 | 97.5% |
| **10⁹** | **0.73212** | **3.807** | **0.542** | **98.0%** |

完整数据表见报告附录。

---

## 🧪 方法

### 计算路径

- **主路径**：C++ 埃氏筛 + 逐偶数扫描 + OpenMP 并行
- **验证路径**：Python/FFT 卷积法（独立实现，算法完全不同）
- **双路验证**：在 17 个尺度上结果一致，相对误差 ≤ 10⁻⁶

### 验证方法

三条独立路径一致指向亚泊松结论：

1. **漂移修正法** — 用零参数漂移律扣除均值漂移
2. **五区块 ANOVA** — 组内方差给出上界 ≤ 0.647
3. **窄窗口实验** — 模型无关测量 κ = 0.620 < 1

---

## ❓ 开放问题

我们提出了若干猜想和开放问题，包括：

1. **亚泊松猜想**：对充分大的 N，Fano 因子 F(N) < 1
2. **κ 极限常数**：κ_noise 是否趋向某个普适常数 κ_∞ ≈ 0.54？
3. **漂移律高阶项**：⟨K⟩ 的渐近展开下一阶是什么？
4. **d(N) 增长律**：对称素数对最小距离的最大值 ~ (log N)^γ, γ ≈ 3.5？
5. **亚泊松机理**：素数对之间的排斥关联来自哪里？

详见报告第 7 章。

---

## 👥 团队

- **luinstein** — 项目发起，主计算，理论分析
- **冷鸢** — 计算工程化，方法学设计，可视化
- **阿岩** — 独立复核，统计方法，批判性审视

**金翼计划 · 耦合刚性研究**

---

## 📜 许可

- 文字内容：[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)
- 代码：MIT License

引用请注明：

> luinstein, 冷鸢, 阿岩. Subpoisson Fluctuations of Goldbach Count: A Numerical Study. Goldwing Research, 2026.

---

## 📮 联系

欢迎提交 Issue / PR，或通过以下方式联系我们：

- GitHub Issues（推荐）

---

## 🔗 相关资源

- [研究报告 v1.6](https://luinstein.github.io/goldwing-research/paper/goldwing_v1.6_subpoisson.html)
- [发布方案](docs/publication_plan_v1.html)
- [素数星空可视化](visualizations/prime_starry_sky.html)
- [金翼星座](visualizations/goldwing_constellation.html)
