---
layout: distill
title: "Survive & Advance: Survival Analysis Applied to March Madness"
description: Some work I've done on applying survival analysis tools to help fill out brackets.
tags:
giscus_comments: true
date: 2025-11-10
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
hidden: true

authors:
  - name: Aaron Foote

bibliography: 2018-12-22-distill.bib

---
- What is censoring
- March Madness has natural censoring, but only a little bit
- When you go to fill out a bracket, you want to know when to eliminate teams
- You aren't really trying to develop a model that predicts individual matchups
- WHY YOU WANT TO USE SURVIVAL ANALYSIS
  - What it gives that other approaches don't
- Non-informative censoring (look into this more)
- Simulation approach to completing a bracket
  * Naive strategies like coin flips and chalk brackets
  * Fit each model + simulate
  * Get distribution of scores
