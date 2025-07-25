---
layout: distill
title: A Mathematical Argument Against Easy Exams
description: A thought experiment, using probability theory, on why exams should not be made easy.
tags:
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

Suppose we have a class of $s$ students, and each of them is given an exam with $n$ questions. We're going to make the following assumptions:

1. Each of the questions is equally difficult, thus each has a probability $p$ of being answered correctly.
2. Each of the students has the same probability $p$ of answering each question correctly.
3. The probabilities of answering the questions correctly are independent.
4. Each student's performance is independent of the others.

Let's review these assumptions. The first two certainly may not reflect reality. Exams usually include softballs to start and a handful of tricky questions at the end, and some students will simply be more knowledgeable about the topic than others. The third assumption is plausible, especially for larger cumulative exams where each question may cover a topic. Lastly, it is reasonable to assume that the performance of one student is independent of the performance of another, assuming they can't communicate during the exam.

With these assumptions in place, the scores on the exam can be treated as following a binomial distribution with parameters $p$ and $n$, givig us some real substance with which to work.


- Describe setup
- Justify setup

- Explain what is to be calculated
- Show the calculations

- Put in sliders + plots
