# AI 使用记录：确认评述论文对象与引用调整

## 基本信息

- 日期：2026-07-06
- 使用工具：Codex
- 任务类型：论文对象确认、项目元信息修正、BibTeX 引用整理
- 涉及文件：`README.md`、`src/main.tex`、`src/references.bib`

## 咨询问题

我们在课程大作业论文列表中选择了第 6 篇 `Optimal resizable arrays`。仓库原先把主评审论文写成 Brodnik 等人在 FOCS 1999 的相关论文，但后续根据课程网页截图和找到的 BibTeX 条目，发现更可能对应的是 Robert E. Tarjan 和 Uri Zwick 在 2023 年发布的 arXiv 论文 `Optimal resizable arrays`。

本次向 AI 咨询的问题是：

1. 课程列表中的 `Optimal resizable arrays` 更可能指哪一篇论文？
2. 用户提供的 Tarjan/Zwick 2023 BibTeX 条目是否可以作为主文献加入 `references.bib`？
3. 仓库中的 README 和 LaTeX 主文件是否需要同步修改？

## AI 辅助结论

AI 根据课程网页截图中的题名、用户提供的 BibTeX 条目以及仓库当前内容进行判断，认为课程列表中的第 6 篇更应以 Tarjan 和 Zwick 2023 年的 `Optimal resizable arrays` 作为主评审对象。

原先 README 中写到的 Brodnik, Carlsson, Munro, Guibas 和 Sedgewick 的 1999 年工作不应作为当前项目的主评审论文，但它是 Tarjan/Zwick 论文的重要相关背景，适合放入相关工作章节中讨论。

## 已执行修改

1. 在 `src/references.bib` 中加入 Tarjan/Zwick 2023 的 BibTeX 条目。
2. 将 `README.md` 中的主评审论文信息改为 Tarjan/Zwick 2023。
3. 在 `README.md` 中保留 Brodnik 等 1999 年工作的背景定位，避免误删相关研究线索。
4. 将 `src/main.tex` 中的测试标题、测试摘要和占位章节改为与 Tarjan/Zwick 2023 论文一致的初始 review 框架。

## 后续待核查

1. 需要继续补充 Brodnik 等 1999 年相关工作的准确 BibTeX 条目。
2. 需要在正文相关工作章节中明确区分主评审论文和前置研究。
3. 需要由组员阅读原论文后，将 AI 辅助判断转化为自己的阅读笔记和正文表述。
