---
layout: distill
title: A Mathematical Argument Against Easy Exams
description: A thought experiment, using probability theory, on why exams should not be made easy.
tags: distill formatting
giscus_comments: false
date: 2025-07-24
featured: false
pretty_table: true
mermaid:
  enabled: true
  zoomable: true
code_diff: true
map: true
chart:
  chartjs: true
  echarts: true
  vega_lite: true
tikzjax: true
typograms: true

authors:
  - name: Aaron Foote

bibliography: 2018-12-22-distill.bib

---

This analysis was inspired by a conversation I had about grades on a midterm exam in a large organic chemistry course. It was pointed out to me that when most students do well on an exam, their grades are clumped together near the top end of the possible scores. Then, even a small deviation in points can result in a large change in rank in the class, resulting in the student's grade in the course potential having considerably more volatility. If, on the other hand, the test was more difficult, one might expect to see the scores more spread out. With this, a small change in score would be less likely to result in a large shift in rank.

It got me thinking about how one might describe this mathematically. After all, this is really a question about comparing variability in the random events of test scores and class rankings. The model I present here is certainly a simplification of the real world, but I think it does a pretty good job of illustrating the concept.

Suppose we have a class of $s$ students, and each of them is given an exam with $n$ questions. The questions

- Describe setup
- Justify setup

- Explain what is to be calculated
- Show the calculations

- Put in sliders + plots
