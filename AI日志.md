# C2 AI 协作日志

> 挑战：C2 AI for Math 论文 · 周期：2026-09-28 · 协作者：学生 + AI
> 记录原则：每一轮 AI 的输入/输出/采纳与否/人工核验结果，均可追溯。

## Round 1 — 材料研读（确定论点）

**AI 输入**：`Lectures on AI for Mathematics.pdf`（同济大学 Xiaoyang Chen & Xiang Jiang，2026/4/11，v1.0）与 `中文论文大纲（AI4Math）.pdf`。

**AI 输出**：提炼出中文大纲的核心命题——「可靠性不能仅依赖最终验证，必须引入中间语义规约层」，并拆出三层结构（生成层 → 语义规约层 → 验证层）与 Typed IR 四要素（Type System / Operational Semantics / Constraints / Composable Graph/AST）。

**采纳情况**：✅ 采纳为论文主论点。**人工核验**：逐条对照了中文大纲原文，三层与 Typed IR 四要素的描述与大纲一致，未发现 AI 自行添加的内容。原文核心结论句「Reliable AI reasoning requires a structured semantic layer」被保留为论文结论。

**教训**：先让 AI 复述材料再比对原文，避免「听起来合理但并非原文主张」的幻觉式概括。

## Round 2 — 文献调研（真实性与可查性）

**AI 输入**：要求检索 AI4Math 可靠性相关一手文献（AlphaProof / AlphaGeometry / LeanDojo / CoT / GSM8K 等），并给出可引用条目。

**AI 输出 / 出现的问题**：Bing 网页检索对学术文献**不可用**——AlphaProof、AlphaGeometry、LeanDojo 的查询只返回广告、百科词条与 spam，无任何可引用的论文页。

**采纳情况**：⚠️ 未采纳检索结果。**人工核验与对策**：改用 arxiv.org/abs/<id> 与 DBLP 直链逐条核验。最终确定的 13 条引用全部为真实、可查的一手文献，逐条核对过作者/标题/venue/年份：

| 键 | 文献 | 核验点 |
|---|---|---|
| wei2022cot | CoT 提示 | NeurIPS 2022，arXiv:2201.11903 |
| cobbe2021gsm8k | GSM8K | arXiv:2110.14168 |
| hendrycks2021math | MATH 数据集 | NeurIPS 2021，arXiv:2103.03874 |
| lewkowycz2022minerva | Minerva | NeurIPS 2022，arXiv:2206.14858 |
| gao2023pal | PAL | ICML 2023，arXiv:2211.10435 |
| chen2022pot | PoT | arXiv:2211.12588 |
| schick2023toolformer | Toolformer | NeurIPS 2023，arXiv:2302.04761 |
| moura2015lean | Lean | CADE-25，DOI:10.1007/978-3-319-21401-6_26 |
| coqmanual | Coq 手册 | coq.inria.fr/refman |
| yang2023leandojo | LeanDojo | NeurIPS 2023，arXiv:2306.15626 |
| trinh2024alphageometry | AlphaGeometry | Nature 625:476–482 |
| wu2022autoformal | Autoformalization | NeurIPS 2022，arXiv:2205.12615 |
| howard1980 | formulae-as-types | Curry 纪念文集 |

**教训**：搜索引擎不等于文献库；学术引用必须回到 arXiv/DBLP/DOI 一手来源核验，否则就是「引用造假」红线。

## Round 3 — 框架构建（原创贡献）

**AI 输入**：要求基于三层模型，给出一个「哪怕很小的原创贡献」。

**AI 输出**：三个原创点——① 把语义规约层从「附属步骤」提升为「中心层」的形式化三层架构；② 五维可靠性清单（Consistency / Derivability / Factual Grounding / Constraint Satisfaction / Traceability）；③ 按「增强了哪一层」对代表性系统的分类法表格 `tab:taxonomy`。

**采纳情况**：✅ 全部采纳。**人工核验**：分类法表格中每个系统的归类依据（CoT 增强生成层、PAL/PoT/Toolformer 增强语义规约层、Lean/Coq 增强验证层）均与该系统论文的原始主张核对过，归类不臆造。

## Round 4 — 论文写作（分 4 段落盘）

**AI 输入**：要求按「摘要/引言/相关工作/方法框架/分析/结论/参考文献」结构产出可编译 paper.tex，分 4 段写入避免单次超长。

**AI 输出**：4 段共 20203 字节——preamble+摘要+引言（4657B）→ Related Work+三层模型（10310B）→ 框架+五维清单+分类表（15879B）→ 工作实例+讨论+结论+`\bibliography{references}`（20203B）。

**采纳情况**：✅ 采纳。**人工核验**：grep 确认 8 个 `\section` 齐备（Introduction / Related Work / A Three-Layer Model / The Bottleneck / Proposed Framework / A Reliability Checklist / Worked Example / Discussion / Conclusion），摘要环境存在，`\cite` 13 键与 references.bib 13 键一一对应。

## Round 5 — 编译与修错

**AI 输入 / 出现的问题**：本机无 TeX 发行版，无 brew。AI 首次尝试下载 tectonic 时用了错误版本 URL（0.15.0），得到 9 字节损坏文件。

**采纳情况 / 对策**：纠正为官方 release 直链（tectonic@0.17.0 aarch64-apple-darwin），下载解压后 `--version` 输出 Tectonic 0.17.0。

**结果**：`/tmp/tectonic/tectonic paper.tex` 编译通过（EXIT=0），生成 72.6KB `paper.pdf`；BibTeX 成功运行，仅有无害的 `Underfull \hbox` 警告。

**教训**：AI 给出的下载链接/命令必须在本机验证后才算数，尤其是跨版本 URL 这类容易「看似正确实则损坏」的地方。

## 一句话总结

本论文的论点、文献、框架、正文、引用库、编译，每一环节都经过「AI 产出 → 人工比对原文/一手来源 → 采纳或修正」的闭环；AI 的两处典型失效（搜索引擎无法替代文献库、版本 URL 错误）均被记录并修正，未流入最终成果。
