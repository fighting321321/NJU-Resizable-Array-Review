# AI 使用记录：辅助完成论文全文精读

## 基本信息

- 日期：2026-07-13
- 使用工具：Codex
- 使用目的：辅助完整阅读 *Optimal resizable arrays* 第 1--10 节，建立可供后续主文写作使用的全文分析索引
- 阅读材料：仓库根目录下的 `paper.pdf`
- 输出位置：`notes/B_notes/paper_reading.md`、`notes/member_B_drafts.md`

## 阅读方式

本次先按 PDF 页码提取全文文本，再按章节重新核对关键定义、定理、伪代码和图示页面。已有的第 2、4--9 节专题笔记被保留，本次新增内容重点是把各部分连接成完整论证链，并补足前置结构、证明依赖、模型限制和结论部分。

## 辅助整理内容

全文分析按以下层次组织：

1. 第 1--10 节逐节概括；
2. Definition 2.1、Theorems 4.1--4.2、6.1、7.3、8.6、9.1 等关键结果的作用；
3. 上界构造、data structuring transformation 和 growth game 下界之间的依赖关系；
4. 每节材料适合写入 `main.tex` 的位置；
5. word-RAM、内存分配、指针表示和 standard implementation 等模型假设；
6. 固定 $r$ 与增长 $r(N)$ 的差别；
7. 原文中疑似笔误和容易误引的参数条件；
8. 接下来成员 B 的主文写作顺序。

## 关键核查结果

本次全文核查特别确认了以下内容：

1. Theorem 4.2 使用 $t(N)$ 的非递减性推出 $s(N)t(N)\geq N$；
2. 第 6 节 rebuild 阈值分别为 $N=B^r$ 和 $N=(B/4)^r$；
3. Lemma 6.3 的 credit 分析分别支付 combine、split 和 rebuild；
4. 第 6.3 节常数访问依赖压缩冗余 base-$B$ 计数器和 `msb`；
5. Theorem 7.3 使用参数 $2r$ 的标准结构，并有 $r\leq\frac12\log N/\log\log N$ 的条件；
6. Theorem 9.1 的直接假设是 $N+O(rN^{1/r})$ 稳定空间和 $r=O(\log N)$；
7. 均摊下界仅对 standard implementations 完整证明；
8. 作者把推广到所有算法以及简化 growth game 下界证明列为开放方向。

## AI 使用边界

AI 用于文本定位、章节归纳、公式核对和写作索引整理。关键公式均回到原 PDF 页面核查；笔记没有直接写入 `src/main.tex`。后续主文仍需分章节重新组织、人工检查引用并与成员 A 内容交叉审阅。

本次开始前 `src/main.pdf` 已存在未提交改动，本次工作没有覆盖该文件。
