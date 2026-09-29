# C2 AI for Math 论文：AI4Math 可靠性框架

> 围绕「AI 做数学」的可靠性问题，产出一篇结构完整、可投稿、可编译的 LaTeX 学术论文。

## 交付物

| 文件 | 说明 |
|---|---|
| `paper.tex` | 论文主文件（8 个 section：摘要/引言/相关工作/三层模型/瓶颈/框架/分析/结论） |
| `references.bib` | BibTeX 引用库，13 篇一手文献（Howard 1980 / de Moura 2015 / Trinh 2024 Nature / Cobbe 2021 GSM8K / Wei 2022 CoT 等） |
| `AI日志.md` | 5 轮 AI 协作日志（每轮输入/输出/采纳/核验可追溯） |
| `AAR.md` | 七维 AAR 复盘（含「AI 误导」案例与对策） |
| `paper.pdf` | 已编译产物（tectonic 0.17.0 编译通过，72.6 KB） |

## 核心论点

生成式模型（CoT）→ 语义规约层（PAL/PoT/Toolformer）→ 形式化验证（Lean/Coq/SMT）的**三层中心化架构**，
外加**五维可靠性清单**与**按层分类法**（`tab:taxonomy`）两个原创贡献。

## 编译

本机无 TeX 发行版时，可用单文件工具链 tectonic 编译：

```bash
tectonic paper.tex
```

产出 `paper.pdf`。
