---
layout: post
title: "VSCode + Stata 17 + AI: Running Your Entire Empirical Workflow in One Window"
date: 2026-04-27
description: "A complete beginner's guide to running end-to-end empirical research seamlessly using AI, eliminating manual formatting and table generation."
cover_image: "/images/blog-stata-ai.png"
permalink: /blog/vscode-stata-ai-en/
lang: en
---

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
