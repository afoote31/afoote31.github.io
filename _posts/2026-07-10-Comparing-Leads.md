---
layout: distill
title: Comparing Leads Across Sports
date: 2026-07-10 16:00:00
featured: false
description: How do leads compare across different sports?
tags: 
categories: 
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
giscus_comments: true
bibliography: 2018-12-22-distill.bib

---

This week, I was listening to the [Wharton Moneyball Podcast](https://open.spotify.com/show/7euXqPldw3dB4gX0HP2J5H?si=d51bd39ac5854adf), a podcast hosted by statistics professors who discuss statistics in sports. Professor [Adi Wyner](https://statistics.wharton.upenn.edu/profile/ajw/) and one of his graduate student collaborators, [Jonathan Pipping](https://www.linkedin.com/in/jdpipping/), mentioned their [research from NESSIS 2025](https://www.youtube.com/watch?v=J0-GQnOtSkI) on win probabilities. While they focused on blown leads, it got me thinking about how different leads might compare in different sports. I want to explore that in this blog post.

#### Basic Setup:
- Data of game scores at minute-level
- Who wins
- Win probabilities, conditional on lead and time remaining for different sports
- Line charts are interesting, might want to explore resampling to get estimates of variability


### Soccer
- Data from lots of leagues
- Reference StatsBomb
- INCLUDE TIES IN COMPUTATION OF WIN PROBABILITIES

<div class="l-page">
  <iframe src="{{ '/assets/plotly/soccer.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>


### Basketball
- Which leagues
- I think it'll be `hoopsR`

<div class="l-page">
  <iframe src="{{ '/assets/plotly/basketball.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

### Football
- I think it'll be `nflFastR`


### Putting it together

I think a table where you can sort by empirical win rates and from there see what sorts of times and leads are comparable. There will be a ton of times so 
