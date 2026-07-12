# AI 使用记录：辅助理解第 5 章下界分析

## 基本信息

- 日期：2026-07-12
- 使用工具：Codex
- 使用目的：辅助阅读论文第 8、9 节，为第 5 章“正确性证明与理论分析”中成员 B 负责的下界部分整理证明框架
- 阅读材料：仓库根目录下的 `paper.pdf`
- 输出位置：`notes/B_notes/paper_reading.md`、`notes/member_B_drafts.md`

## 使用背景

前一阶段已经完成第 4 章空间优化机制初稿，其中介绍了分层块结构、data structuring transformation 和 $O(r)$ 均摊扩缩容上界。第 5 章需要进一步回答这个时间界是否可以继续改进。

由于论文第 8 节对 growth game 的精确求解涉及状态递推、二项式系数和较长的归纳证明，本次使用 AI 工具辅助梳理各个技术结论之间的依赖关系，并区分哪些内容需要写入 review、哪些细节可以保留在阅读笔记中。

## 辅助阅读问题

本次阅读主要围绕以下问题展开：

1. Definition 7.1 中 standard implementation 的条件是什么；
2. 为什么真实可变长数组的块复制过程可以映射到 growth game；
3. $(N,k,\ell)$ 三个参数分别表示什么；
4. 游戏中的三类插入操作及其代价如何定义；
5. Lemma 8.2 为什么能把 $\ell>0$ 的情况约化到 $\ell=0$；
6. Theorem 8.6 的二项式系数公式表达了什么；
7. Corollary 8.13 如何给出可以直接用于下界证明的均摊代价；
8. Theorem 9.1 如何选择 $n=\Theta(r)$ 并推出 $\Omega(r)$；
9. 该下界与第 6 节 $O(r)$ 上界如何匹配；
10. 下界只适用于 standard implementations 会带来什么限制。

## 阶段性理解

本次阅读后，我把论文的均摊时间下界理解为以下证明链：

1. 稳定额外空间限制了数据结构可同时维护的块数、指针数和空闲位置；
2. standard implementation 的块申请与复制行为可以抽象为 growth game 中的合并操作；
3. 即使允许预先知道 $N$、忽略临时空间限制并扩展合并规则，游戏的最优均摊代价仍受到二项式阈值控制；
4. 当稳定额外空间为 $O(rN^{1/r})$ 时，对应游戏参数迫使二项式层级达到 $n=\Theta(r)$；
5. Corollary 8.13 因而给出 $\Omega(r)$ 的均摊代价；
6. 这与论文构造的 $O(r)$ 上界匹配，说明其时间界在 standard implementation 范围内渐近最优。

## 内容取舍

AI 辅助分析后，确定正式正文不需要复现 Theorem 8.6 的完整归纳证明。第 5 章更适合保留以下内容：

- growth game 的模型和操作对应关系；
- Lemma 8.2 的成组插入直觉；
- Theorem 8.6 与 Corollary 8.13 的关键公式；
- 从真实结构到扩展游戏的参数映射；
- 二项式系数估计和 $n=\Theta(r)$ 的选择；
- Theorem 9.1 的结论及 standard implementation 限制。

详细的状态递推、最优终态刻画和 binomial counter 可留在阅读笔记中，正文只说明其作用。

## 人工核查情况

本次整理逐项对照了 `paper.pdf` 中 Definition 7.1、Lemma 8.2、Theorem 8.6、Corollary 8.13、Lemmas 8.17--8.18 和 Theorem 9.1。特别核对了以下容易混淆的内容：

1. 第 9 节的下界假设是稳定空间 $N+O(rN^{1/r})$，而不是只写成 $N+O(N^{1/r})$；
2. 下界只计算元素赋值，并主动忽略其他操作成本；
3. 下界即使不限制 resize 临时空间仍然成立；
4. 最终 $\Omega(r)$ 结论目前只证明到 standard implementations；
5. 第 7 节最终结构使用更小的 $O(N^{1/r})$ 稳定额外空间，因此也受到 Theorem 9.1 的约束。

本次 AI 使用用于辅助论文阅读、公式核对和证明结构整理，没有直接修改 `src/main.tex`。第 5 章正文仍需根据本次笔记另行组织并再次对照原论文检查。
