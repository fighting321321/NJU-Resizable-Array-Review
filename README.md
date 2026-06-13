# 论文评述：最优可变长数组

本仓库包含对理论计算机科学顶级会议会议论文的深度评审与学术评述（Review）：
**"Optimal Resizable Arrays"** (Brodnik et al., FOCS 1999)。

本项目为南京大学《高级数据结构》课程的期末大作业。

---

## 团队成员与贡献矩阵

本项目由两名成员协同完成。根据课程大纲关于“过程分”与“个人贡献trace痕迹”的严格要求，我们的具体分工及在 Git 历史中的追溯区域明确划分如下：

(占位)

---

## 仓库目录结构

本仓库的目录结构严格设计如下：

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

我们团队制定并执行以下同步协议：

1. **独立草稿阶段（Notes 区）：** 在将任何内容正式合并进主论文（`src/main.tex`）之前，所有原始想法、数学推导草稿、大白话理解和伪代码演变，都会高频提交至 `notes/` 目录下各自的文件中。以此确保向老师展现出我们真实、有机的理解演进轨迹。
2. **异步交叉评审（PR 机制）：** 核心学术观点和公式在合并入 `src/main.tex` 时，必须通过 **Pull Request (PR)** 进行。
3. **可追溯的 AI 工具使用：** 我们严格将 AI 工具定位为“互动教科书”，仅用于答疑复杂引理或查询文献。所有向 AI 咨询的硬核记录均会导出为 Markdown 并同步至 `ai_logs/` 文件夹，确保绝对透明。**最终评审论文（final review）中绝不包含任何 AI 代写的文本。**

---

## 评审文献详细信息
* **论文题目：** Optimal Resizable Arrays (最优可变长数组)
* **论文作者：** Andrej Brodnik, Svante Carlsson, J. Ian Munro, Leo J. Guibas, Robert Sedgewick
* **发表会议：** IEEE 40th Annual Symposium on Foundations of Computer Science (FOCS 1999)
* **核心解决问题：** 探讨如何在保证 $O(1)$ 最坏情况随机访问时间、$O(1)$ 均摊插入/删除时间的同时，打破传统数组空间开销随数据量 $N$ 线性增长（$\Theta(N)$）的魔咒，将其死死压制在理论极限下界 $\Theta(\sqrt{N})$ 比特。