# Body Style Unification Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将按成员分区的 LaTeX 草稿统一为结构连续、术语一致、语气正式的论文评述，并提交对应 AI 日志和最新编译 PDF。

**Architecture:** `src/main.tex` 仍作为唯一正文入口，不拆分章节文件。先调整标题和章节衔接，再逐章校订语言，最后新增独立 AI 日志；验证阶段直接生成 `src/main.pdf`，并通过日志扫描和页面渲染确认结果。

**Tech Stack:** LaTeX、XeLaTeX、BibTeX、latexmk、Markdown、Git。

## Global Constraints

- 不重新分配或删除成员贡献记录，贡献信息继续保存在 `README.md`、`Plan_Table.md` 和 Git 历史中。
- 不主动改变已有公式、复杂度结论、引文和论证顺序。
- 统一使用 `\texttt{Get}`、`\texttt{Set}`、`\texttt{Grow}`、`\texttt{Shrink}`。
- 统一使用“均摊时间”“稳定额外空间”“扩缩容临时空间”。
- 聊天使用 `\(...\)`，写入 LaTeX 文件继续使用 `$...$` 和 `\[...\]`。
- 最终提交必须包含与源码一致的 `src/main.pdf`。

---

### Task 1: 调整正文标题与章节边界

**Files:**
- Modify: `src/main.tex`

**Interfaces:**
- Consumes: 已确认的正文语言与结构统一设计。
- Produces: 不含成员分区标记、保持原有七章结构的 LaTeX 正文骨架。

- [x] **Step 1: 记录修改前标题**

Run:

```powershell
Select-String -LiteralPath 'src/main.tex' -Encoding UTF8 -Pattern '^\\section','^\\subsection','^\\subsubsection'
```

Expected: 输出七章及带“成员 A/B”的小节标题。

- [x] **Step 2: 修改标题和合并过程性小节**

Apply these exact structural decisions:

```text
成员 A：问题直觉与论文定位        -> 研究背景与核心问题
成员 B：补充与交叉审阅            -> 论文定位与评述视角
第 2 章的“补充与交叉审阅”        -> 删除标题并把有效句子并入模型导语
成员 B：问题定义与理论模型        -> 模型定义与复杂度目标
成员 A：传统方法与工程背景        -> 摊还分析与传统方法
传统工作                          -> 传统扩缩容策略（降为 subsubsection）
成员 B：理论脉络与下界背景        -> 理论脉络与下界背景
成员 A/B 前缀                     -> 从第 4、5、6 章标题中删除
成员 B：总结                      -> 删除该 subsection，正文直接归入第 7 章
```

- [x] **Step 3: 验证分区标记已经移除**

Run:

```powershell
Select-String -LiteralPath 'src/main.tex' -Encoding UTF8 -Pattern '成员 A','成员 B','补充与交叉审阅'
```

Expected: 无输出。

---

### Task 2: 统一第 1 至第 3 章语言

**Files:**
- Modify: `src/main.tex`

**Interfaces:**
- Consumes: Task 1 形成的标题结构。
- Produces: 正式、连续且不含笔记式元叙述的背景、模型和相关工作章节。

- [x] **Step 1: 改写第 1 章草稿式表达**

Preserve the original claims while applying these replacements:

```text
“也就是：如何维护……”改为陈述式研究问题。
“此问题在工程中与实际中用处广泛”改为动态数组的工程背景。
“更确切说，应该是”改为直接陈述空间界。
“再后面第三节……详细说明”改为“第 3 章将进一步比较相关方法”。
grow/shrink 普通文本统一为 \texttt{Grow}/\texttt{Shrink}。
```

- [x] **Step 2: 将第 2 章补充句并入导语**

Keep the mechanism/strategy connection, but remove “其他暂无补充”。确保 `s(N)`、`t(N)`、word-RAM、数据块和索引块术语与后文一致。

- [x] **Step 3: 整理第 3 章摊还分析段落**

Convert the plain numbered lines into `enumerate`, state that the paper uses aggregate and accounting/credit arguments, and add missing sentence-ending punctuation. Preserve all existing citations.

- [x] **Step 4: 整理传统扩缩容策略段落**

Replace conversational transitions with formal prose, normalize `$N$`, `$C$`, `$(1+\alpha)C$` spacing, and keep the existing asymptotic claims without adding new literature.

- [x] **Step 5: 扫描残留草稿表达**

Run:

```powershell
Select-String -LiteralPath 'src/main.tex' -Encoding UTF8 -Pattern '其他暂无补充','再后面','也就是：','更确切说，应该是','本文中使用的主要是第一种方法'
```

Expected: 无输出。

---

### Task 3: 统一第 4 至第 7 章术语与语气

**Files:**
- Modify: `src/main.tex`

**Interfaces:**
- Consumes: 现有技术推导和 Task 1 的章节标题。
- Produces: 术语、操作名和评述语气一致的核心方法、证明、评价与总结。

- [x] **Step 1: 统一操作名和数据结构术语**

Use `\texttt{Grow}`、`\texttt{Shrink}`、`\texttt{Get}`、`\texttt{Set}` for operation names in prose. Keep algorithm names such as `Combine-Blocks` and `Split-Blocks` in `\texttt{}`.

- [x] **Step 2: 统一中英文表达**

At first occurrence retain explanations such as “冗余 base-$B$ 计数器” and “growth game”；later occurrences use the same form. Replace avoidable first-person narration with objective descriptions while retaining explanatory transitions.

- [x] **Step 3: 统一数学和标点格式**

Remove spaces immediately inside `$...$`, use Chinese full stops after displayed equations where grammatically required, and preserve every equation's mathematical content.

- [x] **Step 4: 检查公式和引用未被删除**

Run:

```powershell
Select-String -LiteralPath 'src/main.tex' -Encoding UTF8 -Pattern '\\cite\{','\\label\{fig:','s\(N\)t\(N\)'
```

Expected: 原有引用和四个 figure label 仍存在，乘积下界仍在正文中。

---

### Task 4: 新增 AI 辅助统一日志

**Files:**
- Create: `ai_logs/2026-07-21_style_unification.md`

**Interfaces:**
- Consumes: Tasks 1–3 的实际修改范围。
- Produces: 可追溯但不复制对话的 AI 使用说明。

- [x] **Step 1: 写入日志结构**

The log must contain these sections:

```markdown
# AI 辅助记录：正文语言与结构统一

## 日期与任务
## 使用目的
## 主要辅助过程
## 人工核验与边界
## 产出与后续检查
```

- [x] **Step 2: 记录实际辅助内容**

State that AI identified title/style inconsistencies, suggested formal rewrites, normalized terminology, and checked compilation. Explicitly state that technical claims, formulas, citations, and contribution records remain subject to manual verification.

- [x] **Step 3: 检查日志不是对话抄录**

Run:

```powershell
Select-String -LiteralPath 'ai_logs/2026-07-21_style_unification.md' -Encoding UTF8 -Pattern '^用户：','^AI：','^User:','^Assistant:'
```

Expected: 无输出。

---

### Task 5: 编译、版面核验和最终提交

**Files:**
- Modify: `src/main.pdf`
- Verify: `src/main.tex`
- Verify: `ai_logs/2026-07-21_style_unification.md`

**Interfaces:**
- Consumes: Tasks 1–4 的最终源码和日志。
- Produces: 与源码一致的 PDF、干净的编译日志和一个完整 Git 提交。

- [x] **Step 1: 直接重新生成仓库 PDF**

Run from `src/`:

```powershell
latexmk -g -xelatex -interaction=nonstopmode -halt-on-error -file-line-error main.tex
```

Expected: exit code 0 and `src/main.pdf` updated.

- [x] **Step 2: 扫描最终编译日志**

Run:

```powershell
Select-String -LiteralPath 'src/main.log' -Pattern 'LaTeX Error','undefined references','Citation .* undefined','Reference .* undefined','Overfull','Underfull','Emergency stop','Fatal error'
```

Expected: 无输出。

- [x] **Step 3: 渲染受影响页面并人工检查**

Render the title page, table of contents, chapter transitions, all figure pages, conclusion, and bibliography. Confirm no overlapping text, detached headings, clipped figures, or blank content pages.

- [x] **Step 4: 检查差异和 Git 状态**

Run:

```powershell
git diff --check
git status --short
```

Expected: only `src/main.tex`, `src/main.pdf`, and `ai_logs/2026-07-21_style_unification.md` are implementation changes; the plan file may also be present if not committed separately.

- [x] **Step 5: 提交最终结果**

Run:

```powershell
git add -- src/main.tex src/main.pdf ai_logs/2026-07-21_style_unification.md docs/superpowers/plans/2026-07-21-body-style-unification.md
git commit -m "unify paper structure and writing style"
```

Expected: commit includes the unified source, compiled PDF, AI log, and implementation plan.
