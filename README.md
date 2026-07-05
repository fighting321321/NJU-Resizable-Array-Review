# 论文评述：最优可变长数组

本仓库包含对理论计算机科学顶级会议会议论文的深度评审与学术评述（Review）：
**"Optimal Resizable Arrays"** (Brodnik et al., FOCS 1999)。

本项目为南京大学《高级数据结构》课程期末大作业。

---

## 团队成员与贡献

成员A：张艺博

成员B：徐黄浩

具体分工见 ./Plan_Table.md

---

## 仓库目录结构

本仓库的目录结构设计如下：

```text
├── README.md               # 项目说明文档（当前文件）
├── .gitignore              # Git 忽略规则文件
├── src/                    # 核心 LaTeX 源码生产区
│   ├── main.tex            # Review 论文主文件（整体论文框架与排版）
│   ├── references.bib      # BibTeX 参考文献库
│   └── figures/            # 存放论文插图
├── notes/                  # 两人各自的原始思维轨迹与草稿
│   ├── member_A_drafts.tex # 同学 A 的草稿
│   └── member_B_drafts.tex # 同学 B 的草稿
└── ai_logs/                # AI 使用日志
```

---

## 工作流规范与学术诚信声明


1. **独立草稿阶段（Notes 区）：** 在将任何内容正式合并进主论文（`src/main.tex`）之前，所有原始想法、数学推导草稿、理解和伪代码，都会提交至 `notes/` 目录下各自的文件中。
2. **异步交叉评审（PR 机制）：** 核心学术观点和公式在合并入 `src/main.tex` 时，通过 **Pull Request (PR)** 进行。
3. **AI 工具使用：** AI 仅用于答疑复杂引理或查询文献。所有 AI 记录会导出为 Markdown 并同步至 `ai_logs/` 文件夹，确保透明。**最终论文中不包含 AI 代写的文本。**

---

## 评审文献详细信息
* **论文题目：** Optimal Resizable Arrays (最优可变长数组)
* **论文作者：** Andrej Brodnik, Svante Carlsson, J. Ian Munro, Leo J. Guibas, Robert Sedgewick
* **发表会议：** IEEE 40th Annual Symposium on Foundations of Computer Science (FOCS 1999)
