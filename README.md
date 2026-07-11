# 论文评述：最优可变长数组

本仓库包含对理论计算机科学论文 **"Optimal resizable arrays"**（Robert E. Tarjan 和 Uri Zwick，2023）的阅读、分析与学术评述（Review）。该工作的初步版本发表于 SOSA 2023，当前项目主要依据 arXiv 完整版本开展阅读和写作。

本项目为南京大学《高级数据结构》课程期末大作业。

---

## 团队成员与贡献

成员A：张艺博

成员B：徐黄浩

具体分工与当前进度见 [`Plan_Table.md`](./Plan_Table.md)。

---

## 仓库目录结构

本仓库的目录结构设计如下：

```text
├── README.md               # 项目说明文档（当前文件）
├── Plan_Table.md           # 论文大纲、成员分工与进度表
├── .gitignore              # Git 忽略规则文件
├── paper.pdf               # 评述对象的论文原文
├── src/                    # 核心 LaTeX 源码生产区
│   ├── main.tex            # Review 论文主文件（成员分区草稿与整体排版）
│   ├── main.pdf            # 当前编译生成的 Review PDF
│   ├── references.bib      # BibTeX 参考文献库
│   └── figures/            # 存放论文插图
├── notes/                  # 两人各自的原始思维轨迹与草稿
│   ├── member_A_drafts.md  # 同学 A 的草稿
│   ├── member_B_drafts.md  # 同学 B 的草稿
│   ├── A_notes/            # 同学 A 的阅读笔记与过程材料
│   │   └── paper_reading.md
│   └── B_notes/            # 同学 B 的阅读笔记与过程材料
│       └── paper_reading.md
└── ai_logs/                # AI 使用日志
```

---

## 工作流规范与学术诚信声明


1. **成员分区写作：** 当前阶段两位成员直接在 `src/main.tex` 中各自标明的成员小节内独立撰写，暂不提前统一写作风格。阅读笔记、推导过程和未定稿材料分别保存在 `notes/A_notes/`、`notes/B_notes/` 及对应成员草稿中。
2. **最终整合与交叉评审：** 各自负责部分形成初稿后，再统一处理章节衔接、术语、公式记号和重复内容。核心学术修改及最终合并通过 Pull Request（PR）进行交叉审阅并保留版本记录。
3. **AI 工具使用：** AI 用于辅助理解论文、梳理写作结构、核查公式与引用以及改进表达。相关使用过程以 Markdown 形式记录在 `ai_logs/` 中；所有写入正文的技术结论均需由成员结合论文原文人工核验。

---

## 评审文献详细信息
* **论文题目：** Optimal Resizable Arrays (最优可变长数组)
* **论文作者：** Robert E. Tarjan, Uri Zwick
* **发表形式：** SOSA 2023 初步版本；arXiv:2211.11009v2，2023
* **论文链接：** [https://arxiv.org/abs/2211.11009](https://arxiv.org/abs/2211.11009)
* **选题来源：** 课程大作业论文列表中的第 6 篇 "Optimal resizable arrays"

