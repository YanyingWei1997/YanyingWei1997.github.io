---
layout: post
title: "VSCode + Stata 17 + AI：一个窗口跑完整个实证研究"
date: 2026-04-27
description: "适合完全零基础的小白，跟着做就能跑通，用 AI 代替繁琐的手工制表和解读。"
cover_image: "/images/blog-stata-ai.png"
---

# 🎯 VSCode + Stata 17 + AI：一个窗口跑完整个实证研究
（适合完全零基础的小白，跟着做就能跑通）

你是不是也有过这种经历——

坐在电脑前，打开 Stata，看着满屏的代码和结果，不知道从哪里下手。想问老师，又怕问题太"小白"。想用 AI 帮忙，AI 说的你听不懂，你想问的又不知道怎么说。

别怕。今天介绍的这套工作流，就是专门来解决这个问题的。

你只需要具备最基本的计量经济学知识（比如知道什么是"X 影响 Y"），剩下的事情——写代码、运行、调格式、生成专业表格——全部可以在一个窗口里让 AI 帮你做。

看完这篇文章，你不需要懂任何编程，不需要用过 VSCode，也不需要了解任何 AI 工具——我会一步一步告诉你每一步该做什么。

> ✨ 请始终铭记：工具只是延伸你的能力，你的学术判断才是核心。

---

## 📋 文章结构导航
1. 这套工作流是什么，能解决什么问题？
2. 正式开始前，你需要准备哪些工具？
3. Stata Workbench 插件详解（重点，看完不再困惑）
4. VSCode + Stata Workbench 插件安装配置（超详细步骤）
5. AI Agent 接入：让 AI 直接操作 Stata
6. 实战演示：让 AI 帮你跑回归、读结果
7. 生成专业的计量经济学表格
8. 初学者最常遇到的 10 个问题（Q&A）
9. 迁移路径：今天做什么，这周做什么

---

## 一、这套工作流是什么？

### 🌟 1.1 先说说你现在的痛点
做实证研究，正常流程是这样的：
- 在 Stata 里写代码
- 跑完回归，满屏是数字
- 截图或者复制结果
- 粘贴到 Word，手动调格式
- 切换到 ChatGPT，粘贴截图，问 AI"这个结果怎么看"
- 再把 AI 的回答复制回 Word
- 如果要跑 Python 或 R，又要导出数据、切换软件……

这个过程里，真正有价值的学术判断只占 10%，剩下 90% 都是机械性的复制粘贴和格式调整。

### 🌟 1.2 我们的目标
用 VSCode + Stata Workbench 插件 + AI Agent，让你在同一个窗口里完成以上所有事情：
- 写 Stata 代码并运行
- 让 AI 直接读取你的数据和分析结果
- 自动生成符合期刊格式的计量表格
- 随时调用 Python 或 R 做补充分析
- 写论文文字时，AI 同步帮你润色

简单来说：**Stata 是引擎，VSCode 是操作台，Stata Workbench 插件是让 AI 和 Stata 互通的桥梁，AI 是坐在你旁边的学长/学姐。**

---

## 二、正式开始前，你需要准备哪些工具？

### 🌟 2.1 工具清单

| 工具                                   | 必须/可选 | 说明                                    |
| -------------------------------------- | --------- | --------------------------------------- |
| Stata 17+                              | 必须      | 电脑里要装好，跑命令全靠它              |
| VSCode 或 Cursor                       | 必须      | 代码编辑器，AI 插件的载体               |
| Stata Workbench 插件                   | 必须      | 插件，让 AI 能操作 Stata 的核心桥梁     |
| AI Agent（Cursor AI / Claude Code 等） | 必须      | AI 助手，理解你的大白话需求并操作 Stata |

---

## 三、Stata Workbench 插件详解（重点，看完不再困惑）
这是整篇文章最关键的概念，也是最多同学最容易困惑的地方。我用这一整节把它讲透。

### 🧭 3.1 什么是 Stata Workbench 插件？
Stata Workbench 是一款 VS Code / Cursor 等编辑器的插件，不是独立软件，也不是 Stata 官方出品。

它由 Thomas Monk（伦敦政治经济学院）开发，发布在 VS Code 插件市场里，任何人都可以免费安装。
- 插件官网：github.com/tmonk/stata-workbench
- VS Code 插件市场搜索关键词：`stata-workbench`（发布者：tmonk）

### 🧭 3.2 这个插件到底能做什么？
它有四个核心功能：

① **在编辑器里直接运行 Stata 代码**
你不需要打开 Stata 的传统界面，只需要在 VS Code 里写 .do 文件，按一个键就能运行，结果直接显示在编辑器底部的面板里。

② **实时查看数据（Data Browser）**
内置 Data Browser 面板，可以实时查看当前加载的数据集，支持筛选和排序。对于检查数据清洗结果特别有用。

③ **AI Agent 能直接操作 Stata**
这是最关键的一点——它支持 MCP 协议（Model Context Protocol）。简单来说，就是 AI 工具（Cursor AI、Claude Code、Codex 等）可以通过这个插件直接给 Stata 发命令、读取运行结果、分析你的数据。
这就是"AI 读懂结果，不需要粘贴"的技术基础。

④ **自动生成图表**
跑 scatter、histogram、regression graph 等命令时，图表会直接以卡片形式出现在面板里，点击就能放大查看。

### 🧭 3.3 支持哪些编辑器？
Stata Workbench 插件支持以下编辑器：
- VS Code（最常用）
- Cursor（AI 代码编辑器，基于 VS Code）
- Windsurf（AI 代码编辑器）
- Antigravity（AI 代码编辑器）
- Claude Code CLI（命令行工具）
- Codex CLI（OpenAI 的代码工具）

换句话说，只要你用的是现代代码编辑器，几乎都能装这个插件。

### 🧭 3.4 这个插件和 Stata 本身是什么关系？
重要的事情说三遍：

**这个插件不能替代 Stata，它只是一个"壳"，帮你把 AI 和 Stata 连接起来。**

你的电脑里必须已经安装 Stata 17 或以上版本。插件只是一个界面，让这个连接过程变得更顺畅。

Stata 17+ 是底层的"发动机"，插件是"方向盘"，AI 是"坐在副驾驶的你"——三者缺一不可。

### 🧭 3.5 Stata Workbench 插件的工作原理
```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   你（用大白话说需求）                                         │
│        ↓                                                     │
│   AI Agent（Cursor AI / Claude Code 等）                      │
│        ↓  ← MCP 协议（Model Context Protocol）               │
│   Stata Workbench 插件                                        │
│        ↓  ← 读写 .do 文件、发送命令、读取结果                  │
│   Stata 17+（真正跑命令的地方）                               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

简单来说：当你在 Cursor 里问 AI "请帮我跑这段回归"，AI 会通过这个插件把你的代码发送给 Stata，把运行结果取回来，再解释给你听。整个过程你不需要切换任何窗口。

---

## 四、VSCode + Stata Workbench 插件安装配置

### 🔍 4.1 第一步：确认电脑里装了 Stata 17+
这是前提条件，插件本身不包含 Stata。

- Mac：打开"访达" → "应用程序" → 找到 Stata 文件夹，确认有 Stata 17 或 18 的图标。
- Windows：在开始菜单搜索"Stata"，确认有 Stata 17 或 18。

如果没有，去学校图书馆或授权账户下载安装（Stata 16 不支持此插件）。

### 🔍 4.2 第二步：下载并安装 VSCode 或 Cursor
**方案 A：用 Cursor（推荐小白，一步到位）**
Cursor 内置了 AI，直接装好就能用，比 VS Code + 插件的配置更简单。
1. 打开 cursor.com
2. 点击 Download，选择 macOS 或 Windows 版本
3. 安装完成，打开即可

**方案 B：用 VS Code（更通用）**
1. 打开 code.visualstudio.com
2. 点击 Download，安装完成

### 🔍 4.3 第三步：在编辑器里安装 Stata Workbench 插件
以 Cursor 为例（VS Code 步骤完全一样）：
1. 按 Cmd+Shift+X（Mac）或 Ctrl+Shift+X（Windows）打开扩展市场
2. 在搜索框里输入：`stata-workbench`
3. 找到发布者为 tmonk 的插件
4. 点击绿色的 "Install" 按钮

安装完成后，左边竖条会多出一个 Stata 图标，底部面板会增加 Stata Terminal 和 Data Browser 两个标签页。

### 🔍 4.4 第四步：运行第一行 Stata 代码
1. 按 Cmd+N（Mac）或 Ctrl+N（Windows）新建文件
2. 右下角点击"纯文本" → 搜索 Stata，选择它
3. 输入代码：
```stata
sysuse auto, clear
summarize
```
4. 点击编辑器右上角的 ▶ 运行按钮

### 🔍 4.5 第五步：设置 Stata 路径
第一次运行会提示设置 Stata 路径。

- Mac 路径示例：
  `/Applications/Stata.app`
- Windows 路径示例：
  `C:\Program Files\Stata18\StataSE64.exe`

查找方式：
- Mac：右键 Stata → "显示包内容" → Contents/MacOS/StataSE
- Windows：右键 Stata 图标 → "打开文件所在位置"

设置完成后，重新运行。

### 🔍 4.6 验证是否配置成功
运行代码后，底部出现类似结果即为成功：
```
(1978 automobile data)
. summarize
    Variable |        Obs        Mean    Std. Dev.       Min        Max
-------------+---------------------------------------------------------
        make |          0
       price |         74    6,065.2    2,949.5       3,291      15,906
         mpg |         74      21.3     5.785           12         41
      rep78 |         69       3.4     .9893            1          5
```

🎉 恭喜你，Stata 已经在你的编辑器里跑起来了！

---

## 五、AI Agent 接入：让 AI 直接操作 Stata

### 🛠️ 5.1 方案一：直接用 Cursor 内置 AI（最简单，推荐小白）
如果你用的是 Cursor，它已经内置了 AI，不需要任何额外配置。

使用方法：
1. 按 Cmd+L（Mac）或 Ctrl+L（Windows）打开 AI 对话框
2. 用大白话描述需求
3. AI 生成代码后，按 Cmd+Enter 运行

### 🛠️ 5.2 方案二：VS Code + Claude Code CLI
前提：已安装 Stata Workbench 插件 + Claude Code CLI
配置步骤：
1. VS Code 设置中搜索 `stataMcp.configureClaudeCode`
2. 设置为 Enabled
3. 重启 Claude Code 面板

使用：终端输入 `claude`，直接指挥 Stata。

### 🛠️ 5.3 方案三：VS Code + Cline + ChatGPT API
1. 扩展市场安装 Cline
2. 填入你的 OpenAI API Key
3. 启用 stataMcp 相关配置

> ⚠️ API Key 安全提醒：不要泄露、不要粘贴到聊天框让 AI 处理。

---

## 六、实战演示：让 AI 帮你跑回归、读结果

### 🌟 6.1 场景一：让 AI 帮你写 Stata 代码
你对 AI 说：
> 我有一份企业数据，包含 500 家上市公司 2015-2022 年的财务报表变量。被解释变量（Y）是 ROA，核心解释变量（X）是数字化转型指数，控制变量包括企业规模、资产负债率、固定资产比例，用双向固定效应模型回归。请帮我写 Stata 代码。

AI 生成示例代码：
```stata
* 数据预处理
encode stkcd, gen(stock_id)
xtset stock_id year
gen ln_size = ln(size)
gen lev = debt / assets

* 双向固定效应基准回归
xtreg ROA digital_index ln_size lev tangibility i.year, fe robust
est store 基准回归

* 异质性分析
xtile size_median = ln_size, n(2)
bysort size_median: xtreg ROA digital_index ln_size lev tangibility i.year, fe robust
est store 异质性规模
```

### 🌟 6.2 场景二：让 AI 帮你读懂回归结果
你对 AI 说：
> 请帮我解读这个回归结果。digital_index 的系数 0.038 表示什么？R-squared = 0.423 在企业数据中算什么水平？最后一行 rho = 0.629 代表什么含义？

AI 会直接解读结果，无需截图粘贴。

### 🌟 6.3 场景三：让 AI 帮你做稳健性检验
你对 AI 说：
> 请为上面的基准回归做三类稳健性检验：① 替换被解释变量（用 ROE 替代 ROA）；② 缩尾处理 1% 的极端值；③ 工具变量法（用行业平均数字化指数作为工具变量）。

AI 生成完整稳健性检验代码。

---

## 七、生成专业的计量经济学表格

### 🌟 7.1 什么是 esttab？
esttab 是 Stata 官方风格的表格输出命令，需要先安装：
```stata
ssc install estout, replace
```

### 🌟 7.2 让 AI 帮你生成表格代码
你对 AI 说：
> 请用 esttab 把上面基准回归和三组稳健性检验的结果合成一张主表，参考《经济研究》格式：保留 3 位小数，显著性用星号标注，在表格下方加注。

AI 生成代码：
```stata
esttab 基准回归 替换ROE 缩尾处理 IV using "回归结果表.rtf" ///
    , b(3) se(3) star(* 0.1 ** 0.05 *** 0.01) ///
    replace r2 abs(#) ///
    title("数字化转型对企业盈利能力的影响") ///
    addnotes("注：括号内为稳健标准误；* p<0.1, ** p<0.05, *** p<0.01") ///
    drop(ln_size lev tangibility i.year _cons) ///
    indicate("年份固定效应 = i.year") ///
    rtf
```

运行后直接得到可粘贴进 Word 的规范表格。

---

## 八、初学者最常遇到的 10 个问题（Q&A）

**Q1：我的 Stata 是盗版，会有问题吗？**
A：可以运行基本命令，但兼容性不保证。建议使用学校正版授权。

**Q2：Cursor 的 AI 回复有次数限制吗？**
A：免费版有限制，Pro 版无限制；也可用 Cline + API Key。

**Q3：我的数据是 Excel 文件，怎么导入 Stata？**
A：`import excel "文件路径.xlsx", firstrow clear`

**Q4：运行 Stata 时出现 "no observations" 是什么意思？**
A：无有效观测，常见原因：变量名错、路径错、筛选后无数据。

**Q5：我没有面板数据，能用这套工作流吗？**
A：可以，横截面 OLS 同样适用。

**Q6：AI 给我写的代码，我完全看不懂，能直接用吗？**
A：不建议直接用于论文。先让 AI 解释，理解后再使用。

**Q7：插件装好了，但运行时提示"CLI missing"怎么办？**
A：命令面板搜索 `Stata: Install MCP CLI helper` 安装。

**Q8：面板数据怎么判断用固定效应还是随机效应？**
A：用 Hausman 检验，p<0.05 用固定效应。

**Q9：同时用 Python 和 Stata，数据怎么传递？**
A：`python: import statause("my_data.dta")`

**Q10：AI 给了明显错误的结果怎么办？**
A：以你的学术判断为准，查阅教材或请教老师同学。

---

## 九、迁移路径：今天做什么，这周做什么

**今天（5 分钟）**
去 cursor.com 下载并安装 Cursor，熟悉 AI 对话界面。

**这周（30 分钟）**
- 安装 Stata Workbench 插件
- 导入自己的 .do 文件并运行
- 让 AI 帮你解读一次回归结果

**这月（2 小时）**
- 用 AI 完成基准回归 + 稳健性检验
- 用 esttab 生成正式表格
- 尝试让 AI 同步阅读文献、提炼观点

工具永远只是工具。好的工具，能让你把 100% 的精力集中在研究设计和学术判断上——而不是浪费在复制粘贴和调格式上。

祝你研究顺利。✨

---

- 本文适用：Stata 17+，Cursor 或 VS Code + Claude Code/Cline。

- 插件地址：github.com/tmonk/stata-workbench

<br><br>

---
---

<br>

# 🌐 English Version

*(Perfect for absolute beginners. Follow along and you'll get it running!)*

Have you ever experienced this?

Sitting in front of your computer, opening Stata, staring at a screen full of code and results, and not knowing where to start. You want to ask your professor, but you're afraid the question is too "basic". You try to use AI, but the AI gives you code you don't understand, and you don't know how to prompt it correctly.

Don't panic. The workflow introduced today is specifically designed to solve this problem.

You only need basic econometrics knowledge (like knowing what "X affects Y" means). The rest—writing code, executing it, adjusting formats, and generating professional tables—can all be done by AI in a single window.

After reading this article, you don't need to know any programming, you don't need to have used VSCode before, and you don't need to understand complex AI tools. I will walk you through exactly what to do at each step.

> ✨ **Always remember: Tools only extend your capabilities. Your academic judgment remains the core.**

---

## 📋 Table of Contents
1. What is this workflow, and what problems does it solve?
2. What tools do you need to prepare before starting?
3. Stata Workbench Plugin Explained (Crucial, no more confusion after this)
4. VSCode + Stata Workbench Installation & Configuration (Detailed Steps)
5. AI Agent Integration: Letting AI Control Stata
6. Practical Demonstration: Letting AI Run Regressions & Read Results
7. Generating Professional Econometrics Tables
8. Top 10 Questions for Beginners (Q&A)
9. Migration Path: What to do today, what to do this week

---

## I. What is this workflow?

### 🌟 1.1 Let's start with your current pain points
Normally, empirical research goes like this:
- Write code in Stata
- Run the regression, get a screen full of numbers
- Screenshot or copy the results
- Paste them into Word, manually adjust the formatting
- Switch to ChatGPT, paste the screenshot, and ask "How do I interpret this?"
- Copy the AI's response back to Word
- If you need to run Python or R, you have to export data, switch software...

In this process, true academic judgment only accounts for 10%. The remaining 90% is mechanical copying, pasting, and formatting.

### 🌟 1.2 Our Goal
By using VSCode + Stata Workbench Plugin + AI Agent, you can do all the following in the **same window**:
- Write and run Stata code
- Let AI directly read your data and analysis results
- Automatically generate econometric tables that meet journal formatting standards
- Seamlessly call Python or R for supplementary analysis
- Let AI help you polish your writing as you draft your paper

Simply put: **Stata is the engine, VSCode is the dashboard, the Stata Workbench plugin is the bridge connecting AI and Stata, and AI is the senior researcher sitting next to you.**

---

## II. What tools do you need to prepare?

### 🌟 2.1 Tool Checklist

| Tool                                   | Required/Optional | Description                                    |
| -------------------------------------- | --------- | --------------------------------------- |
| Stata 17+                              | Required  | Must be installed on your computer. It runs the commands. |
| VSCode or Cursor                       | Required  | Code editor, the carrier for AI plugins. |
| Stata Workbench Plugin                 | Required  | The core bridge that allows AI to operate Stata. |
| AI Agent (Cursor AI / Claude Code, etc.)| Required  | The AI assistant that understands your plain language and operates Stata. |

---

## III. Stata Workbench Plugin Explained

### 🧭 3.1 What is the Stata Workbench Plugin?
Stata Workbench is an extension for editors like VS Code / Cursor. It is not standalone software, nor is it officially produced by StataCorp.
It was developed by Thomas Monk (LSE) and is published in the VS Code Marketplace. Anyone can install it for free.
- GitHub: github.com/tmonk/stata-workbench
- Extension search keyword: `stata-workbench` (Publisher: tmonk)

### 🧭 3.2 What does this plugin actually do?
It has four core functions:

① **Run Stata code directly in the editor**
You don't need to open the traditional Stata interface. Write your `.do` files in VS Code, press a shortcut, and the results appear in the bottom panel.

② **Real-time Data Viewer (Data Browser)**
It has a built-in Data Browser panel to view the currently loaded dataset in real-time, supporting filtering and sorting. Great for checking data cleaning results.

③ **Allows AI Agents to directly operate Stata**
This is the most critical point. It supports the MCP (Model Context Protocol). Simply put, AI tools can send commands directly to Stata, read the results, and analyze your data through this plugin. This is the technical foundation for "AI reading results without pasting."

④ **Automatically generate charts**
When you run commands like `scatter`, `histogram`, etc., the charts will appear directly as cards in the panel.

### 🧭 3.3 What's the relationship between this plugin and Stata?
Important: **This plugin cannot replace Stata. It is just a "shell" that connects AI and Stata.**
You must have Stata 17+ installed on your computer. 

### 🧭 3.4 How it works
```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   You (describing needs in plain English)                   │
│        ↓                                                    │
│   AI Agent (Cursor AI / Claude Code)                        │
│        ↓  ← MCP Protocol                                    │
│   Stata Workbench Plugin                                    │
│        ↓  ← Reads/writes .do files, sends commands          │
│   Stata 17+ (Where the commands actually run)               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```
You ask AI to run a regression, AI sends the code to Stata, retrieves the results, and interprets them for you. All without switching windows.

---

## IV. Installation & Configuration

### 🔍 Step 1: Ensure Stata 17+ is installed
- Mac: Check `Applications` folder.
- Windows: Search Start Menu.

### 🔍 Step 2: Download VSCode or Cursor
**Option A: Cursor (Highly recommended for beginners)**
Cursor has built-in AI. 
1. Go to cursor.com
2. Download and install.

**Option B: VS Code**
1. Go to code.visualstudio.com

### 🔍 Step 3: Install the Plugin
1. Open the Extensions Marketplace (Cmd+Shift+X or Ctrl+Shift+X).
2. Search for `stata-workbench`.
3. Click "Install".

### 🔍 Step 4: Run your first Stata code
1. Create a new file (`Cmd+N` / `Ctrl+N`).
2. Set language to Stata.
3. Type:
```stata
sysuse auto, clear
summarize
```
4. Click the ▶ Run button in the top right.

### 🔍 Step 5: Set Stata Path
The first time you run it, it will ask for your Stata path.
- Mac: `/Applications/Stata/StataSE.app`
- Windows: `C:\Program Files\Stata18\StataSE64.exe`

---

## V. AI Agent Integration

### 🛠️ Method 1: Cursor's Built-in AI (Easiest)
If you use Cursor, AI is already built-in.
1. Press `Cmd+L` (Mac) or `Ctrl+L` (Windows) to open AI Chat.
2. Describe your request in plain English.
3. Let AI generate the code and run it.

### 🛠️ Method 2: VS Code + Claude Code CLI
1. Enable `stataMcp.configureClaudeCode` in VS Code settings.
2. Type `claude` in the terminal to command Stata.

---

## VI. Practical Demonstration

### 🌟 Scenario 1: Letting AI write Stata code
Prompt:
> "I have firm-level data for 500 listed companies from 2015-2022. The dependent variable is ROA, the core independent variable is the digital transformation index. Control variables are firm size, leverage, and tangibility. Use a two-way fixed effects model. Please write the Stata code."

### 🌟 Scenario 2: Letting AI interpret results
Prompt:
> "Please interpret this regression result. What does the 0.038 coefficient for the digital index mean? Is an R-squared of 0.423 considered good for corporate data?"

### 🌟 Scenario 3: Letting AI run robustness checks
Prompt:
> "Please run three robustness checks for the baseline regression: 1) Replace the dependent variable with ROE; 2) Winsorize at the 1% level; 3) Instrumental Variable approach using the industry average."

---

## VII. Generating Professional Tables

### 🌟 7.1 What is esttab?
`esttab` is a command for outputting publication-quality tables. Install it first:
```stata
ssc install estout, replace
```

### 🌟 7.2 Letting AI generate the table code
Prompt:
> "Please use esttab to combine the baseline regression and the three robustness checks into one main table formatted for an academic journal. Keep 3 decimal places, indicate significance with stars, and add a footnote."

AI will output the `.rtf` or `.doc` table perfectly formatted.

---

## VIII. Q&A

**Q1: Will this work if my Stata isn't genuine?**
A: Basic commands will run, but compatibility isn't guaranteed. Recommend using a university license.

**Q2: Does Cursor's AI have usage limits?**
A: The free version does, Pro is unlimited. You can also use Cline + API Keys.

**Q3: How do I import Excel data into Stata?**
A: `import excel "filepath.xlsx", firstrow clear`

**Q4: What does "no observations" mean?**
A: No valid data found. Check your variable names, paths, or filtering conditions.

**Q5: Can I use this workflow if I don't have panel data?**
A: Yes, cross-sectional OLS works perfectly too.

**Q6: Should I directly use code from AI if I don't understand it?**
A: Not for papers. Ask AI to explain it first. Once you understand the logic, use it.

**Q7: How to choose between Fixed Effects and Random Effects?**
A: Use the Hausman test. If p < 0.05, use Fixed Effects.

**Q8: How to transfer data between Python and Stata?**
A: Use `python: import statause("my_data.dta")`

**Q9: What if AI gives obviously wrong results?**
A: Always trust your academic judgment. Consult textbooks or professors when in doubt.

---

## IX. Migration Path

**Today (5 mins)**
Go to cursor.com, download and install Cursor, and familiarize yourself with the AI chat interface.

**This Week (30 mins)**
- Install the Stata Workbench plugin
- Import your own `.do` file and run it
- Let AI interpret a regression result for you

**This Month (2 hours)**
- Use AI to complete a baseline regression + robustness checks
- Generate a formal table using `esttab`
- Experiment with having AI read literature and extract key points simultaneously

Tools are just tools. A good tool lets you focus 100% of your energy on research design and academic judgment—instead of wasting time copying, pasting, and formatting.

Best of luck with your research! ✨

---
*Applicable to: Stata 17+, Cursor or VS Code + Claude Code/Cline.*
*Plugin link: github.com/tmonk/stata-workbench*
