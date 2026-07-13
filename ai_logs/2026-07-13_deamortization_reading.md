# AI 使用记录：辅助理解去摊还化限制

## 基本信息

- 日期：2026-07-13
- 使用工具：Codex
- 使用目的：辅助研究论文中 $O(r)$ 均摊扩缩容时间为何一般不能通过 background rebuilding 转换为 worst-case，并区分该问题与 Theorem 9.1 均摊下界的关系
- 阅读材料：仓库根目录下的 `paper.pdf`
- 输出位置：`notes/B_notes/paper_reading.md`、`notes/member_B_drafts.md`

## 使用背景

前一天已经完成 growth game 和 $\Omega(r)$ 均摊下界的阅读笔记，但论文引言还提出一个需要单独解释的判断：扩缩容时间一般不能改成 worst-case，除非 $r=2$。如果直接把这个判断归因于 Theorem 9.1，会混淆均摊下界与去摊还化所需空间之间的区别。

本次使用 AI 辅助对照论文引言、Sitarski HAT、Brodnik 等人的结构以及结论部分，梳理 background rebuilding 在本文两类空间模型下受到的限制。

## 辅助研究问题

本次主要讨论以下问题：

1. 普通动态数组为什么可以通过 background rebuilding 去摊还化；
2. 后台迁移期间同时存在的新旧表示应计入哪一类空间；
3. 第 6 节最高层块的大小为什么是 $\Theta(N^{1-1/r})$；
4. 当 $r>2$ 时，该块为什么超过 $O(N^{1/r})$ 的稳定额外空间预算；
5. 为什么 $r=2$ 时不存在同样的指数差距；
6. Sitarski 和 Brodnik 等人的 $N+O(\sqrt{N})$ 结构如何支持 worst-case 更新；
7. Theorem 9.1 实际证明了什么，哪些更强结论不能由它直接推出；
8. standard implementation 限制应如何在 review 中评价。

## 阶段性理解

本次整理后形成了以下理解：

1. background rebuilding 通过把一次大规模复制拆分到多个操作中来降低单次更新时间；
2. 尚未完成的新表示会在操作之间持续存在，因此属于稳定状态的一部分，不能继续记作单次 resize 的临时空间；
3. 对论文的一般 $r$ 构造，后台迁移可能需要持久保存 $\Theta(N^{1-1/r})$ 的新块；
4. 当 $r>2$ 时，$N^{1-1/r}$ 严格大于允许的 $N^{1/r}$ 稳定额外空间，所以常规后台重建会破坏目标空间界；
5. 当 $r=2$ 时两个空间量级均为 $\Theta(\sqrt{N})$，这与已有 worst-case 结构相容；
6. Theorem 9.1 证明的是 standard implementations 的 $\Omega(r)$ 均摊下界，并未单独证明不存在 $O(r)$ worst-case 的所有非标准实现；
7. 因此正文应把“均摊最优性”和“常规去摊还化的空间障碍”作为两个相关但不同的论点。

## 内容安排

本次研究结果计划用于两个位置：

- 第 5 章结尾：说明 $\Omega(r)$ 均摊下界与 worst-case 问题的区别，并解释常规 background rebuilding 为什么不适用；
- 第 6 章局限性：说明下界目前只覆盖 standard implementations，对一般非标准算法仍缺少完整形式化证明。

## 人工核查情况

本次逐项对照了 `paper.pdf` 中以下内容：

1. 引言关于普通倍增数组可以 background rebuild 的说明；
2. 引言关于一般构造不能改成 worst-case、除非 $r=2$ 的表述；
3. 第 3.2 节关于 HAT 同时使用两种块大小进行后台重建的说明；
4. 第 3.3 节关于 Brodnik 等人结构达到 $O(1)$ worst-case 更新的说明；
5. 第 9 节 Theorem 9.1 的 standard implementation 均摊下界；
6. 第 10 节关于下界适用范围和非标准算法猜想的讨论。

AI 用于辅助区分论证层次、检查指数关系和组织笔记，没有修改 `src/main.tex`。当前 `src/main.pdf` 在本次工作开始前已有未提交改动，本次也没有覆盖该文件。
