---
layout: distill
title: Failed Research Ideas
description: A running list, with descriptions, of ideas I had for research that ultimately fell flat (and why).
tags:
giscus_comments: true
date: 2025-08-11
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

Most of the ideas I have don't turn out to be worth pursuing, but that doesn't mean good work wasn't done! I'm going to be putting as many of these failed ideas as I can in this post, with the hope that it is a useful resource to others. If you're reading something and think I made a mistake or believe there is a way to overcome the roadblock that stopped me, I would be delighted to hear about it in the comments.

## Restricting Coalitions of Shapley Values to Improve Efficiency
Over the summer I chatted with [Professor Luca de Alfaro](https://luca.dealfaro.com/bio.html) a few times about research, and one of the topics was related to Shapley values. Additionally, I'm working as a data scientist with the [Center for Motivation and Change: Foundation for Change](https://cmcffc.org/), a nonprofit related to therapy and substance abuse. The nonprofit offers trainings in their evidence-based techniques, and the trainings go for a handful of weeks. Surveys are administered before beginning the training, as well as at the end. 

A question we could be interested in answering is how each week contributes to the overall learning of clients. One might opt for hierarchical linear modeling approaches or panel designs, but I thought that Shapley values might be a possible approach. By treating each week of the training as a player in a cooperative game, you can estimate the contribution of each week to overall learning by considering coalitions. This sort of setup, with a series of sessions in which learning or growth is the goal, occurs frequently. Corporate trainings, school, or skills-based therapies such as cognitive behavioral therapy are common examples. Coalitions naturally arise due to people missing sessions. While it would require some investigation, I don't think it's entirely implausible that absences would be completely at random ([MCAR](https://www.ncbi.nlm.nih.gov/books/NBK493614/))<d-cite key="mcar"></d-cite> or close enough to completely at random to make the method useful in many settings.

In practice, Shapley values are difficult to estimate because they require considering all $2^n$ coalitions for a game that has $N$ players. For a game with value function $v$ and set of players $N$, the Shapley value for player $i$ is defined as

$$
\varphi_i(v) = \sum_{S\subseteq N \setminus \{i\}} \frac{\vert S \vert ! (n - \vert S \vert - 1)!}{n!}[v(S \cup \{i\}) - v(S)] = \frac{1}{n}\sum_{S\subseteq N \setminus \{i\}} \binom{n-1}{\vert S \vert}^{-1}[v(S \cup \{i\}) - v(S)].
$$

In our case, the exponential number of coalitions is particularly distressing due to the small sample size of the surveys. This would lead to Shapley value estimates with considerable variance. Additionally, Shapley values don't naturally consider ordering when distinguishing between coalitions. Now, there has been work on modifications to Shapley values that consider orderings or players <d-cite key="orderedShap1"></d-cite><d-cite key="orderedShap2"></d-cite><d-cite key="orderedShap3"></d-cite>, but considering the ordering simply results in a further increase in the number of coalitions. 

In the setting of trainings however, each coalition can only occur in one order, since the trainings are offered in successive weeks. Furthermore, a participant is typically not allowed to miss as many sessions as they would like. An organizer may inform pariticipants that the outset that they are not allowed to miss more than $k$ sessions or they are removed. This is a very natural thing to do, as those who do not attend enough sessions are likely to miss out on synergistic elements across weeks and not properly represent learning. Again, I assumed missingness completely at random. 

With these observations, I decided to restrict the coalitions used to compute Shapley values to only those for which less than $k$ sessions missed. Now, we have a *polynomial* number of coalitions for which to estimate Shapley values! Thinking that I had adapted Shapley values for this setting in a way that makes them computationally feasible, I was eager to start proving axioms such as efficiency, symmetry, and so on.



- Utility of Shapley values
- Their difficulties
- Intuition of my idea
- Settings where it could be used
- Set up the formulation (example?)
- Why it fails
