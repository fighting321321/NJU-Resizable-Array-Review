# 成员 B 草稿

## 一、我的整体定位

我在本次 review 中主要负责把 Tarjan 和 Zwick 的 *Optimal resizable arrays* 讲成一个严谨的数据结构模型和复杂度证明故事。成员 A 更偏向问题直觉、传统动态数组背景和整体技术路线；我需要补足形式化定义、相关工作中的理论脉络、下界证明、增长游戏（growth game）以及论文贡献的批判性评价。

从最终论文结构来看，我的重点章节是：

- 第 2 章：问题定义与理论模型；
- 第 3 章：文献调研与相关工作中的理论背景、后续定位；
- 第 4 章：本文核心方法中的空间区分与优化机制；
- 第 5 章：正确性证明与理论分析中的下界部分；
- 第 6 章：创新点、局限性、批判性分析和后续影响；
- 第 7 章：参考文献整理与引用格式统一。

## 二、阅读笔记索引

论文初步阅读笔记已单独整理到 `notes/B_notes/paper_reading.md`。后续更细的模型推导、下界证明和 growth game 理解也优先追加到该文件，本文件只保留个人计划和任务拆分。

## 三、当前进展记录

### 2026-07-08：第 2 章问题模型初稿

今天已将论文第 2 节相关内容整理进 `src/main.tex` 的“问题定义与理论模型”章节，完成了一个可继续精修的正文初稿。当前版本主要覆盖：

- resizable array 的抽象接口；
- 只允许末端 `Grow` / `Shrink` 的模型限制；
- data block、index block、auxiliary block 的内存块模型；
- $(s(N),t(N))$-implementation 的定义；
- 稳定存储空间和扩缩容临时空间的区分；
- 本文后续时间--空间 trade-off 的复杂度目标。

这部分还需要后续人工精修，尤其是术语统一、与第 1 章的衔接，以及是否需要增加原论文 Definition 2.1 的引用说明。

### 2026-07-09：第 3 章下界背景初稿

今天将论文第 4 节中 Brodnik et al. 的 $N+\Omega(\sqrt{N})$ 空间下界，以及 Tarjan/Zwick 推出的 $s(N)t(N)=\Omega(N)$ 乘积下界，整理进 `src/main.tex` 的“文献调研与相关工作”章节。

这一段目前的定位是相关工作和论文动机：它解释为什么已有 $N+O(\sqrt{N})$ 结构看似遇到瓶颈，以及 Tarjan/Zwick 为什么要把空间拆成 storing/accessing space 和 temporary resizing space 两类。第 5 章后续再写 growth game、$\Omega(r)$ 均摊下界和更正式的证明分析。

### 2026-07-11：第 4 章核心方法阅读准备

今天没有继续精修第 3 章，而是转向第 4 章“本文核心方法”中我负责的空间优化机制部分。已阅读论文第 5、6、7 节，并把可用于正文的理解整理到 `notes/B_notes/paper_reading.md`。

本次阅读重点是：

- 第 5 节的 $(O(N^{1/3}), O(N^{2/3}))$ 特例；
- 第 6 节中一般 $r$ 的分层块结构和冗余 base-$B$ 计数器；
- 为什么标准结构先得到 $O(rN^{1/r})$ 平时额外空间；
- 第 7 节 data structuring transformation 如何把平时额外空间进一步压到 $O(N^{1/r})$；
- 哪些内容适合写进第 4 章，哪些证明细节应留到第 5 章。

下一步如果继续写正文，我应该优先把这些笔记整理成第 4 章 B 小节“空间优化机制”的初稿。

### 2026-07-11：第 4 章空间优化机制初稿

在前一阶段阅读笔记的基础上，已将第 4 章中成员 B 负责的“空间优化机制”写入 `src/main.tex`。正文目前按四个层次组织：

1. 用 $r=3$ 特例解释大块与小块如何交换稳定空间和临时空间；
2. 推广到一般 $r$ 的分层块结构和冗余 base-$B$ 计数器；
3. 简要说明 $O(1)$ 最坏情况访问与 $O(r)$ 均摊扩缩容时间的来源；
4. 介绍第 7 节 data structuring transformation，并核对最终结果需要使用参数为 $2r$ 的标准结构。

本次正文暂不展开 credit 分析、growth game 和 $\Omega(r)$ 下界，以免与第 5 章重复。下一步应进入第 5 章下界分析的精读和笔记阶段。

## 四、近期优先任务

### 任务 1：精修第 2 章“问题定义与理论模型”

第 2 章已经写入 `src/main.tex`，下一步不是从零写，而是精修和核查。需要对照论文第 2 节检查 resizable array 的抽象接口，确认 `Length`、`Get`、`Set`、`Grow`、`Shrink` 等操作的描述准确，其中 `Grow` 和 `Shrink` 只发生在数组末端。这一点很重要，因为如果允许在任意位置插入和删除，问题会变成动态序列维护，复杂度边界也不同。

这一章需要写清楚：

- 固定数组、动态数组、栈式可变长数组和双端可变长数组之间的关系；
- 为什么普通连续内存数组扩容时必须重新申请并复制；
- 本文的时间目标：按下标访问为 $O(1)$ worst-case；
- 本文的空间目标：区分存储状态空间和扩缩容时的临时空间；
- 论文中 $(s(N),t(N))$-implementation 的定义。

### 任务 2：整理第 3 章相关工作的理论线索

成员 A 负责传统 dynamic array、doubling 和基本摊还分析。我负责进一步梳理 Tarjan/Zwick 论文中提到的前置工作和理论背景，包括：

- Sitarski 的 hashed array tree (HAT)；
- Brodnik et al. 的 $N+O(\sqrt{N})$ 空间结构；
- Brodnik et al. 给出的 $N+\Omega(\sqrt{N})$ 下界；
- succinct data structures 背景；
- 动态序列、tiered vectors、fast dynamic arrays 等相关研究。

这一部分的目标不是堆引用，而是解释 Tarjan/Zwick 为什么要重新区分 “storing/accessing space” 和 “temporary resizing space”。

当前进度：已先写入 Brodnik et al. 的 $N+\Omega(\sqrt{N})$ 下界和 Tarjan/Zwick 的 $s(N)t(N)=\Omega(N)$ 下界视角，后续还需要补 Sitarski、HAT 和 succinct data structures 的引用与背景。

### 任务 3：解释论文的关键新视角

Tarjan/Zwick 的重要贡献不是简单否定 Brodnik 等人的下界，而是把空间分成两类：

- 平时为了存储数组并支持访问需要占用的空间；
- 执行 `Grow` 或 `Shrink` 时短暂需要的临时空间。

论文声称对任意整数 $r\ge 2$，可以做到：

$$
\text{存储空间} = N + O(N^{1/r}),
$$

同时在扩缩容时允许短暂使用：

$$
\text{临时空间} = N + O(N^{1-1/r}).
$$

在这个设定下，按下标访问仍然是 $O(1)$ worst-case，而 `Grow` 和 `Shrink` 的均摊代价是 $O(r)$。我需要把这一点写成第 4 章中的“优化机制”部分，并和 A 写的整体结构衔接起来。

### 任务 4：攻克第 5 章下界分析

这是我负责的最核心技术部分。需要重点阅读论文第 4、8、9 节，整理以下问题：

- Brodnik et al. 的 $N+\Omega(\sqrt{N})$ 下界直觉是什么；
- 为什么这个下界约束的是不区分临时空间时的整体空间；
- Tarjan/Zwick 如何扩展这个下界视角；
- growth game 抽象了什么操作过程；
- 为什么当存储空间限制为 $N+O(N^{1/r})$ 时，`Grow` 的均摊代价至少是 $\Omega(r)$；
- 为什么一般不能把 $O(r)$ amortized 的扩缩容时间去摊还化成 worst-case，除非 $r=2$。

这一章写作时要避免只照搬公式。我需要先写出直觉解释，再补公式化证明框架。

## 五、我负责的正文产出

1. 在 `src/main.tex` 中补充第 2 章初稿。（已完成初稿，待精修）
2. 在第 3 章中补充 Sitarski、Brodnik et al. 和 succinct data structures 的相关工作段落。
3. 在第 4 章中补充 storing space 与 temporary space 的区分。
4. 在第 5 章中补充下界证明、growth game 和 $\Omega(r)$ 均摊下界。
5. 在第 6 章中补充创新点、局限性和后续影响分析。
6. 维护 `src/references.bib`，确保所有引用都能在正文中对应出现。

## 六、参考文献整理计划

当前 `references.bib` 已经加入 Tarjan/Zwick 2023 的主文献。后续我需要继续补齐：

- Brodnik et al. 的 resizable arrays 相关论文；
- Sitarski 的 HAT 文章或可引用资料；
- CLRS 中 dynamic tables 的章节；
- Dietz 关于 list indexing 的工作；
- Fredman and Saks 关于 cell-probe lower bounds 的论文；
- Bille et al. 关于 fast dynamic arrays 的论文；
- 论文中其他用于比较动态序列或动态数组的相关文献。

## 七、记录方式

我的正文草稿可以直接写入 `src/main.tex` 中对应章节，但推导过程、没完全想清楚的证明和文献核查记录应继续保留在本文件中。这样既方便后续修改，也能保留从阅读、理解到写作的过程记录。

近期最小可交付目标：

1. 先完成第 2 章问题模型草稿；（已完成初稿）
2. 再完成第 3 章下界背景和相关工作初稿；（已开始）
3. 完成第 4 章核心方法中空间优化机制的阅读笔记；（已完成初步整理）
4. 完成第 5 章 growth game 与均摊下界的阅读笔记；
5. 最后补充关键参考文献，并把正文引用打通。
