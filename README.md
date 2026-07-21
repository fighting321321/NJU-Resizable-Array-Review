# 论文评述：最优可变长数组

本仓库包含对理论计算机科学论文 **"Optimal resizable arrays"**（Robert E. Tarjan 和 Uri Zwick，2023）的阅读、分析与学术评述（Review）。该工作的初步版本发表于 SOSA 2023，当前项目主要依据 arXiv 完整版本开展阅读和写作。

本项目为南京大学《高级数据结构》课程期末大作业。

当前正文已经完成第一轮统一整合：七章主体内容、图示、参考文献和总结均已写入 `src/main.tex`，成员分区标签、术语、公式记号和语言风格已经统一。项目现处于后续文献补充、技术交叉审阅和最终交付阶段。

---

## 团队成员与贡献

成员A：张艺博

成员B：徐黄浩

具体分工与当前进度见 [`Plan_Table.md`](./Plan_Table.md)。

---

## 仓库目录结构

本仓库的目录结构设计如下：

```text
├── README.md                # 项目说明文档（当前文件）
├── Plan_Table.md            # 论文大纲、成员分工、进度与终审任务
├── .gitignore               # Git 忽略规则
├── paper.pdf                # 本地论文原文，不纳入 Git
├── src/                     # LaTeX 正文与交付文件
│   ├── main.tex             # 已统一整合的 Review 主文件
│   ├── main.pdf             # 当前编译生成并纳入版本控制的 Review PDF
│   ├── references.bib       # BibTeX 参考文献库
│   └── figures/             # 正文插图及对应生成源码
├── notes/                   # 成员草稿、阅读笔记与推导材料
│   ├── member_A_drafts.md
│   ├── member_B_drafts.md
│   ├── A_notes/
│   └── B_notes/
├── ai_logs/                 # AI 辅助使用记录
└── docs/superpowers/        # 统一修改的设计与执行记录
```

---

## 当前进度与后续任务

已经完成：

- 七章正文、四幅图示、总结和参考文献的第一轮整合；
- 成员分区标签、章节衔接、术语、公式记号和语言风格统一；
- LaTeX 全文编译与 PDF 版面检查；
- 阅读笔记、个人草稿、图表源码和 AI 使用日志的过程留痕。

下一阶段：

- 检索并核验论文发表后的相关研究，补充第 3 章和第 6 章；
- 由两位成员结合原论文交叉核对构造、参数范围、上下界条件和结论边界；
- 核对摘要、标题页信息、引用顺序和最终 PDF；
- 通过 PR 完成最终学术审阅并保留合并记录。

具体任务状态见 [`Plan_Table.md`](./Plan_Table.md)。

---

## 编译方法

项目使用 XeLaTeX 和 BibTeX。安装 TeX Live 或其他包含 `latexmk`、XeLaTeX 与 BibTeX 的 LaTeX 发行版后，在仓库根目录执行：

```powershell
cd src
latexmk -xelatex -interaction=nonstopmode -halt-on-error main.tex
```

编译结果为 `src/main.pdf`。辅助文件由 `.gitignore` 忽略，最终 PDF 需要与对应的 LaTeX 源文件一起提交。

---

## 工作流规范与学术诚信声明

1. **贡献记录：** 前期按照成员分工独立阅读和撰写，原始材料保存在 `notes/`，主要贡献和当前状态记录在 `Plan_Table.md`，正文统一后不再用成员标签分割论述。
2. **交叉评审：** 语言和结构统一不代替技术审阅。两位成员需要结合论文原文检查彼此负责部分，核心学术修改及最终合并通过 Pull Request（PR）保留审阅记录。
3. **AI 工具使用：** AI 用于辅助理解论文、梳理写作结构、核查公式与引用以及改进表达。相关使用过程以 Markdown 形式记录在 `ai_logs/` 中；所有写入正文的技术结论均需由成员结合论文原文人工核验。

过程材料与计划表中的记录项对应如下：

| 记录项 | 仓库材料 |
| ------ | -------- |
| 小组分工说明 | `Plan_Table.md` |
| 阅读笔记与论文批注 | `notes/A_notes/`、`notes/B_notes/` |
| 文献调研记录 | `notes/`、`src/references.bib` |
| 图表与推导过程 | `src/figures/`、`notes/A_notes/assets/` |
| 交叉审阅记录 | Git 提交历史与最终 PR |
| AI 使用记录 | `ai_logs/` |

---

## 评审文献详细信息
* **论文题目：** Optimal Resizable Arrays (最优可变长数组)
* **论文作者：** Robert E. Tarjan, Uri Zwick
* **发表形式：** SOSA 2023 初步版本；arXiv:2211.11009v2，2023
* **论文链接：** [https://arxiv.org/abs/2211.11009](https://arxiv.org/abs/2211.11009)
* **选题来源：** 课程大作业论文列表中的第 6 篇 "Optimal resizable arrays"

