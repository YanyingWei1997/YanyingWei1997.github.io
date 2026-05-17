---
layout: post
title: "Claude/Codex + Zotero MCP + Linter + LaTeX：把参考文献从“AI 生成”改成“AI 核查”"
date: 2026-05-17
description: "一套更稳的参考文献自动化流程：AI 只负责候选，Zotero 管理文献，Linter 清洗元数据，Better BibTeX 导出 verified.bib。"
cover_image: "/images/blog-zotero-mcp-linter-latex.svg"
permalink: /blog/zotero-mcp-linter-latex/
lang: zh
translation_key: zotero-mcp-linter-latex
categories:
  - research-notes
---

# Claude/Codex + Zotero MCP + Linter + LaTeX：把参考文献从“AI 生成”改成“AI 核查” 📚

现在很多人已经开始用 Claude、Codex、ChatGPT 来写论文、做综述、整理开题报告。

这件事本身没问题。

但是，**参考文献不能靠 AI “看起来像”**。

标题、作者、年份、DOI、摘要，只要有一个对不上，这条文献就不能直接放进论文。尤其是 AI 生成 BibTeX 时，很容易出现一种很隐蔽的问题：

**DOI 是真的，但 DOI 对应的不是它给出的那篇文章。**

所以，参考文献自动化的重点，不是让 AI 更快地“编出文献”。

而是把流程改成：

```text
AI 负责找候选文献
Zotero 负责管理文献
Zotero Linter 负责清洗元数据
Zotero MCP 负责让 AI 读取 Zotero
Better BibTeX 负责导出稳定的 verified.bib
Word / Markdown / LaTeX 负责最终插入引用
```

简单说，就是：

> **AI 可以生成 bib，但最好只作为候选 bib。  
> 最终进入论文正文的 verified.bib，建议从 Zotero 中已经核查过的 collection 导出。**

这篇文章就用小白能看懂的方式，讲一下如何把 **Claude/Codex + Zotero MCP + Zotero Linter + Better BibTeX + LaTeX** 组合起来，搭一个更稳的参考文献自动化流程。🚀

---

## 一、先搞清楚：这里的 Linter 是 Zotero 插件，不是代码工具 🧩

很多人一看到 Linter，会想到写代码时用的 ESLint、Pylint、Ruff。

但这里说的不是这些。

这里说的是 **Zotero 里的 Linter 插件**。

它的作用是帮你清洗 Zotero 里的文献条目，比如：

```text
标题格式是否规范
期刊名是否统一
DOI 字段是否干净
日期、卷号、页码是否规范
是否有重复条目
条目类型是否异常
```

也就是说，**Linter 是放在 Zotero 里面用的**。

它不是帮你写论文，也不是帮你判断一篇文章是否适合你的研究。

它主要负责一件事：

> **先把 Zotero 里的文献条目变干净。**

这套流程里，每个工具的分工可以这样理解：

```text
Claude / Codex：帮你找文献、整理文献、核查文献
Zotero：你的文献仓库
Zotero Linter：帮你清洗 Zotero 条目
Zotero MCP：让 AI 能读取或操作 Zotero
Better BibTeX：生成稳定 citekey，并导出 .bib 文件
Word / Markdown / LaTeX：最终写论文和插参考文献
```

最关键的一句话是：

> **AI 不是最终裁判。AI 只能提供候选文献。**

真正能进入正文的文献，必须经过 Zotero 清洗、DOI 核查、abstract 核查和人工复查。

---

## 二、AI 能生成 bib，为什么还要 Zotero 导出？🤔

这个问题很重要。

很多人会问：

> 既然 AI 已经能自动生成 BibTeX，为什么还要导入 Zotero？为什么还要 Better BibTeX 导出？

答案是：

```text
AI 生成的 bib = 候选 BibTeX
Zotero / Better BibTeX 导出的 bib = 经过文献库管理后的正式 BibTeX
```

AI 当然可以生成 `.bib`。

但它更适合做“入口”，不适合做“最终出口”。

因为 AI 生成的 BibTeX 本质上是一段一次性文本。

后面如果你修改了标题、作者、期刊名、DOI、abstract、citekey，AI 那份 `.bib` 不会自动同步。

而 Zotero 是你的文献数据库。

你在 Zotero 里修正文献，Better BibTeX 可以把已经核查过的 collection 自动导出为 `verified.bib`。

这样后面写 LaTeX、Markdown 或 Overleaf 时，就不容易出现：

```text
正文 citekey 和文献库对不上
文献已经改了，但 bib 文件没更新
候选文献混进了正式参考文献
重复条目没有清理
DOI 字段格式不统一
```

所以更稳的理解是：

```text
AI 生成 bib：方便导入
Zotero 管理 bib：方便长期维护
Better BibTeX 导出 bib：方便正式写作引用
```

如果只是写一个临时小作业，AI 生成 BibTeX 后人工检查，也可以用。

但如果是论文、开题报告、投稿、博士申请材料，建议不要跳过 Zotero 和 Better BibTeX 这一步。

一句话总结：

> **AI 可以生成候选 bib。  
> 但最终论文使用的 verified.bib，最好来自 Zotero 中已经核查过的 verified collection。**

---

## 三、为什么不能直接让 AI 生成最终参考文献？⚠️

很多人会直接对 AI 说：

```text
帮我找 20 篇相关文献，并生成 BibTeX。
```

看起来很省事。

但问题也在这里。

AI 给出的参考文献，经常会有三类风险：

```text
第一类：标题是假的
第二类：DOI 是假的
第三类：标题和 DOI 都是真的，但它们不是同一篇文章
```

第三类最麻烦。

因为 DOI 能打开，标题也像一篇真实论文，肉眼扫一眼很容易放过去。

但是，只要 DOI 跳转后的文章，和 BibTeX 里的标题、年份、作者对不上，这条参考文献就是错的。

所以要记住：

```text
有 DOI ≠ 文献一定正确
DOI 能打开 ≠ 这条引用可以用
AI 给出 BibTeX ≠ 可以直接放进论文
Zotero 里有这篇文献 ≠ 已经核查过
```

这套流程的核心原则是：

> **候选文献可以由 AI 找，但最终参考文献必须经过核查。**

---

## 四、完整流程是什么样？🧭

先看完整流程图。

```text
确定研究主题
↓
Claude / Codex 根据提示词拆分 3–4 个研究方向
↓
每个方向先找 12–15 篇候选文献
↓
AI 生成候选 BibTeX，或整理 DOI / PMID / arXiv ID
↓
候选文献导入 Zotero
↓
进入 00_AI_Candidates
↓
Zotero Linter 清洗元数据
↓
人工或 AI 初筛，剔除明显不相关文献
↓
Better BibTeX 生成稳定 citekey
↓
Zotero MCP 让 Claude / Codex 回读 Zotero 条目
↓
核查 DOI、标题、年份、作者、abstract
↓
通过核查的条目进入 02_Verified_For_Manuscript
↓
Better BibTeX 自动导出 verified.bib
↓
Word / Markdown / LaTeX 只引用 verified.bib 里的 citekey
↓
最终人工抽查核心引用
```

如果用一句话解释，就是：

> **AI 先找候选，Zotero 管起来，Linter 先清洗，DOI 和 abstract 再核查，最后只引用 verified.bib。**

这里有一个小优化：

原来很多人每个方向只让 AI 找 8–10 篇候选文献。

但实际操作中，有些会因为 DOI 错误、abstract 缺失、作者不一致、不是期刊论文、主题不够相关而被剔除。

所以建议：

```text
每个方向先找 12–15 篇候选文献
最终保留 5–8 篇高质量文献
其中近 5 年文献不少于 3 篇
```

这样更稳。

---

## 五、Zotero 里怎么建文件夹？📁

为了让小白不乱，建议在 Zotero 里先建 4 个 collection。

也就是 4 个文献文件夹：

```text
00_AI_Candidates
01_Linter_Checked
02_Verified_For_Manuscript
99_Rejected
```

它们分别是什么意思？

### 1. `00_AI_Candidates`

这里放 AI 找出来的候选文献。

注意：**这里的文献不能直接引用。**

它们只是候选，还没有核查。

### 2. `01_Linter_Checked`

这里放经过 Zotero Linter 清洗后的文献。

这一步说明条目的格式更干净了。

但它们仍然不一定可以引用。

因为还没有完成 DOI、标题、作者、年份、abstract 的核查。

### 3. `02_Verified_For_Manuscript`

这里放最终可以进入正文的文献。

正文只能引用这里面的文献。

### 4. `99_Rejected`

这里放被剔除的文献。

为什么要保留？

因为以后 AI 可能又找出同一篇，你可以马上知道它之前为什么被排除。

建议同时加一些标签：

```text
ai-candidate
linter-checked
doi-ok
abstract-ok
metadata-match
metadata-mismatch
no-abstract
not-journal
recent-5y
verified
rejected
```

小白一开始不用全部标签。

先用 5 个就够了：

```text
ai-candidate
linter-checked
verified
rejected
no-abstract
```

---

## 六、最重要的提示词：不要让 AI 自由发挥 ✍️

这一步非常关键。

如果你只说“帮我找文献”，AI 很容易给你一堆看起来完整、但没有核查过的结果。

所以要给 AI 一段固定提示词。

你可以直接复制下面这段：

```text
你是文献检索与引用核查助手。

请帮我检索【研究主题】相关文献，期刊论文优先。

工作流程如下：

1. 先按研究方向拆分主题，建议拆成 3–4 个方向。
2. 每个研究方向先寻找 12–15 篇候选文献。
3. 候选文献优先选择 journal article。
4. 只保留有 DOI 的候选文献。
5. 如果能获取 DOI / PMID / arXiv ID，优先保留这些标识符，方便导入 Zotero。
6. DOI 必须可以通过以下形式正常解析：

   https://doi.org/{DOI}

7. abstract 必须可以核实。
8. 标题、年份、作者姓名必须与 DOI 跳转结果一致。
9. 不要把 preprint、conference paper、book chapter 默认当作期刊论文。
10. 如果使用 preprint、conference paper 或 book chapter，必须单独标注原因。
11. AI 可以先生成候选 BibTeX，但只能作为候选，不是最终 verified.bib。
12. 候选文献需要导入 Zotero 的 00_AI_Candidates collection。
13. 候选文献进入 Zotero 后，需要先经过 Zotero Linter 插件处理。
14. Linter 处理后，再通过 Zotero MCP 回读 Zotero 条目。
15. 对每条文献进行二次核查：
    - DOI 是否有效；
    - DOI 跳转结果是否与标题一致；
    - 年份是否一致；
    - 作者姓名是否一致；
    - abstract 是否可以核实；
    - 是否为正式期刊论文；
    - 是否真的支持正文中的论点；
    - 是否属于近 5 年文献。
16. 每个研究方向最终保留不少于 5 篇正确文献。
17. 每个研究方向近 5 年文献不少于 3 篇。
18. 通过核查的文献写入 02_Verified_For_Manuscript。
19. 被剔除的文献写入 99_Rejected，并说明剔除原因。
20. 最终论文使用的 verified.bib，应从 Zotero 的 02_Verified_For_Manuscript collection 通过 Better BibTeX 导出。
21. verified.bib 必须包含 abstract 字段。
22. 每个研究方向单独输出 BibTeX 代码块和核查说明。
23. 不要输出 DOI 无法解析、abstract 无法核实、标题/年份/作者与 DOI 结果不一致的条目。
```

这段提示词的重点不是“多找文献”。

而是给 AI 加上限制。

它会强制 AI 注意：

```text
有没有 DOI
DOI 能不能打开
标题对不对
年份对不对
作者对不对
abstract 能不能核实
是不是期刊论文
近 5 年文献够不够
是否真的支持正文论点
```

这一步越严格，后面出错越少。

---

## 七、为什么 DOI 和 abstract 一定要核查？🔍

DOI 可以理解成论文的“身份证号”。

但问题是：

> **身份证号是真的，不代表它一定属于这篇文章。**

所以不能只看 DOI 是否存在。

还要检查：

```text
DOI 对应的标题是否一致
DOI 对应的年份是否一致
DOI 对应的作者是否一致
DOI 对应的期刊是否一致
abstract 是否可以从可靠来源核实
这篇文献是否真的支持正文观点
```

举个例子。

AI 给你一条 BibTeX：

```bibtex
@article{example2024,
  title = {AI Tools in Academic Writing},
  author = {Smith, John},
  year = {2024},
  doi = {10.xxxx/abc123}
}
```

你打开 DOI 以后发现，DOI 对应的真实文章是：

```text
Title: Machine Learning in Medical Diagnosis
Author: Brown, David
Year: 2021
```

那这条文献就不能用。

即使 DOI 能打开，也不能用。

abstract 也一样。

如果 Zotero、出版社页面、Crossref、PubMed、期刊官网都查不到 abstract，那就不能让 AI 自己编一个。

要直接标记：

```text
no-abstract
```

最终进入 BibTeX 的 abstract，必须来自可以核实的来源。

BibTeX 里建议保留 abstract 字段：

```bibtex
@article{smith2024example,
  title = {Example Title},
  author = {Smith, John and Wang, Li},
  journal = {Example Journal},
  year = {2024},
  volume = {12},
  number = {3},
  pages = {100--120},
  doi = {10.xxxx/example},
  abstract = {This study examines ...}
}
```

为什么要保留 abstract？

因为后面你还可能让 Claude/Codex 做这些事：

```text
按主题整理文献
判断文献是否支持某个观点
写 literature review
总结研究方法
比较不同论文的结论
生成引文说明
```

这些任务都需要知道文章讲了什么。

所以 abstract 很重要。

---

## 八、Word、Markdown 和 LaTeX 三种写作路线 🧱

参考文献怎么插入，要看你用什么写论文。

一般有三条路线。

---

### 1. Word 路线：适合大多数小白

如果你主要用 Word 写论文，建议走半自动路线。

```text
AI 找候选文献
↓
文献进入 Zotero
↓
Zotero Linter 清洗
↓
Zotero MCP / 人工核查
↓
进入 02_Verified_For_Manuscript
↓
用 Zotero Word 插件插入引用
```

这里要注意：

> **不要让 AI 直接改 Word 里的 Zotero 引用字段。**

因为 Zotero 在 Word 里的引用不是普通文字，而是动态字段。

更稳的方式是：

```text
AI 告诉你该引用哪些文献
你用 Zotero Word 插件正式插入引用
Zotero 自动生成文末参考文献
```

这条路线最适合刚开始用 Zotero 的同学。

---

### 2. Markdown 路线：适合写技术报告和开题报告

如果你用 Markdown 写作，可以直接用 citekey。

正文里这样写：

```markdown
近年来，AI 辅助文献检索开始进入科研写作流程，但参考文献幻觉仍然需要额外核查 [@smith2024; @wang2023]。
```

然后用 Pandoc 生成 Word：

```bash
pandoc manuscript.md \
  --citeproc \
  --bibliography=refs/verified.bib \
  -o manuscript.docx
```

这里的核心规则是：

```text
正文只能引用 verified.bib 里的 citekey
```

如果某个 citekey 不在 verified.bib 里，就不要引用。

---

### 3. LaTeX 路线：适合正式论文和期刊投稿

如果你写的是正式论文、英文期刊论文、博士申请研究计划，LaTeX 路线更稳。

流程是：

```text
Zotero + Better BibTeX 导出 verified.bib
↓
LaTeX 正文引用 verified.bib 中的 citekey
↓
BibTeX / Biber 生成参考文献表
```

正文里可以这样引用：

```latex
Recent studies have discussed the reliability risks of AI-assisted academic writing \citep{smith2024example,wang2023example}.
```

如果你使用 `natbib`，可以这样写：

```latex
\documentclass[12pt]{article}

\usepackage[round,authoryear]{natbib}

\begin{document}

Recent studies have discussed the reliability risks of AI-assisted academic writing \citep{smith2024example,wang2023example}.

\bibliographystyle{apalike}
\bibliography{refs/verified}

\end{document}
```

编译顺序一般是：

```bash
pdflatex manuscript.tex
bibtex manuscript
pdflatex manuscript.tex
pdflatex manuscript.tex
```

如果你使用 `biblatex`，可以这样写：

```latex
\documentclass[12pt]{article}

\usepackage[backend=biber,style=apa]{biblatex}
\addbibresource{refs/verified.bib}

\begin{document}

Recent studies have discussed the reliability risks of AI-assisted academic writing \parencite{smith2024example,wang2023example}.

\printbibliography

\end{document}
```

编译顺序一般是：

```bash
pdflatex manuscript.tex
biber manuscript
pdflatex manuscript.tex
pdflatex manuscript.tex
```

如果你用 Overleaf，可以直接把 `verified.bib` 上传到项目里。

然后正文只引用 `verified.bib` 里的 citekey。

不要引用候选文献里的 citekey。

---

## 九、Claude / Codex 在 LaTeX 里怎么帮你？🤖

LaTeX 写作里，Claude/Codex 不应该直接“编参考文献”。

它应该帮你做三件事。

### 第一步：识别哪里需要文献

你可以先在 `.tex` 文件里写占位符：

```latex
AI-assisted literature search may improve writing efficiency, but it can also introduce citation hallucination when bibliographic metadata is not verified. % <需要文献: AI-assisted academic writing; citation hallucination; bibliographic metadata verification>
```

### 第二步：让 AI 根据占位符找候选文献

你可以这样给 Claude/Codex 下指令：

```text
请扫描 manuscript.tex 中所有 <需要文献: ...> 标记。

对每个标记执行以下步骤：

1. 判断这个位置需要支持什么论点。
2. 按主题检索候选文献。
3. 期刊论文优先。
4. 每个方向先找 12–15 篇候选文献。
5. 只保留有 DOI 的候选文献。
6. AI 可以生成候选 BibTeX，但只作为候选，不作为最终 verified.bib。
7. 将候选文献导入 Zotero 的 00_AI_Candidates。
8. 等 Zotero Linter 清洗完成。
9. 通过 Zotero MCP 回读清洗后的条目。
10. 核查 DOI、标题、年份、作者、abstract。
11. 只把通过核查的条目写入 02_Verified_For_Manuscript。
12. 通过 Better BibTeX 自动导出 verified.bib。
13. 用 verified.bib 中的 citekey 替换对应占位符。
14. 输出 rejected list，说明被剔除文献的原因。
```

### 第三步：让 AI 替换 citekey

替换前：

```latex
AI-assisted literature search may improve writing efficiency, but it can also introduce citation hallucination when bibliographic metadata is not verified. % <需要文献: AI-assisted academic writing; citation hallucination; bibliographic metadata verification>
```

替换后：

```latex
AI-assisted literature search may improve writing efficiency, but it can also introduce citation hallucination when bibliographic metadata is not verified \citep{smith2024example,wang2023example}.
```

这里有一个硬规则：

```text
Claude / Codex 只能插入 verified.bib 中存在的 citekey。
```

如果 citekey 不在 verified.bib 里，就不能插入正文。

这一步可以防止 AI 在 LaTeX 里乱写一个不存在的 citekey。

---

## 十、被剔除的文献和核查报告也要保留 🗂️

很多人做文献筛选时，只保留最终结果。

这不够。

被剔除的文献也应该保留。

原因很简单：

```text
第一，避免重复劳动
第二，方便以后追溯
第三，方便给导师或合作者解释
```

建议记录成这样：

```text
Rejected Literature Log

1. Title: xxx
   DOI: xxx
   Reason: DOI resolves, but title does not match.

2. Title: xxx
   DOI: xxx
   Reason: Abstract not verifiable.

3. Title: xxx
   DOI: xxx
   Reason: Not a journal article; conference paper.

4. Title: xxx
   DOI: xxx
   Reason: Year mismatch between BibTeX and DOI landing page.

5. Title: xxx
   DOI: xxx
   Reason: Author mismatch.
```

除了 rejected list，我还建议增加一份 `verification_report.md`。

它可以记录每条文献的核查状态：

```text
Title match: yes / no
Author match: yes / no
Year match: yes / no
DOI resolves: yes / no
Abstract verified: yes / no
Journal article: yes / no
Used in manuscript: yes / no
```

如果你用 Markdown 或 LaTeX 写作，可以这样组织项目：

```text
paper-project/
├── manuscript.tex
├── manuscript.md
├── AGENTS.md
├── CLAUDE.md
├── refs/
│   ├── candidates/
│   │   ├── ai_literature_search.bib
│   │   ├── citation_hallucination.bib
│   │   └── doi_metadata_validation.bib
│   ├── verified.bib
│   └── rejected.md
├── notes/
│   ├── verification_report.md
│   └── search_log.md
└── output/
    └── manuscript.pdf
```

这里最重要的是三份文件：

```text
candidates/*.bib：候选文献
verified.bib：最终可引用文献
rejected.md：剔除记录
```

正文只能引用 `verified.bib`。

不要引用 `candidates/*.bib`。

---

## 十一、总结：参考文献自动化，不是少检查，而是把检查固定下来 ✅

这套流程的关键，不是让 AI 自动生成参考文献。

而是让 AI 进入一个受控流程。

```text
Claude / Codex 负责检索和整理
Zotero 负责管理文献
Zotero Linter 负责清洗元数据
Zotero MCP 负责让 AI 回读和写入 Zotero
Better BibTeX 负责稳定 citekey 和 BibTeX 导出
Word / Markdown / LaTeX 负责最终插入和排版
```

最终目标是：

```text
找得到
查得动
对得上
能入库
能引用
能追溯
```

参考文献最怕的不是少。

而是不准。

所以，不要让 AI 直接决定参考文献。

更稳的方式是：

```text
AI 先找候选
Zotero 管起来
Linter 先清洗
DOI 和 abstract 再核查
Better BibTeX 自动导出 verified.bib
最后只引用 verified.bib
```

如果你用 Word，就用 Zotero 插件插入正式引用。

如果你用 Markdown，就用 Pandoc 和 `verified.bib` 生成参考文献。

如果你用 LaTeX，就用 Better BibTeX 导出 `verified.bib`，再用 BibTeX 或 Biber 编译。

最后再强调一次：

```text
AI 不是不能生成 bib。
AI 可以生成候选 bib。
但最终进入论文正文的 verified.bib，应该来自 Zotero 中已经核查过的 verified collection。
```

这样，AI 才真正变成一个可用的科研写作助手。

不是一个会生成漂亮假引用的文本工具。📚
