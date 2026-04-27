---
title: "Using ChatGPT to Support Literature Review Workflows"
date: 2023-04-27
description: "A note on using Python and ChatGPT to collect CNKI literature records, score papers, merge abstracts, and generate structured literature-review summaries."
---

This note summarizes a workflow for combining Python scripts with ChatGPT to support literature review tasks, including CNKI literature collection, paper scoring, abstract merging, and structured synthesis.

The original Chinese article was published on the WeChat official account **三分甜的涠**:

[用ChatGPT写文献综述相关代码（知网篇）](https://mp.weixin.qq.com/s/9BHUBNRGR-qV0UkRmcmQlA)

The workflow includes four steps:

1. Collect literature metadata and abstracts with Python.
2. Score papers by citation frequency, download frequency, and additional relevance signals.
3. Merge high-quality papers into a text file for model-assisted reading.
4. Prompt ChatGPT to classify findings and produce cited literature-review summaries.

This workflow is designed for applied research projects where the literature base is large and an initial screening stage can improve reading efficiency.
