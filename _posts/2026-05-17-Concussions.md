---
layout: distill
title: CTE as an Occupational Health Problem
date: 2026-05-17 17:30:00
featured: false
description: Through simulation, I demonstrate the healthy worker survivor bias in measuring concussion risk.
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

##### Intro to CTE
- Risk when playing football
- Can come from concussions, but also from repeated subconcussive injuries
- Discovered by Dr. Bennet Omalu<d-cite key="Omalu1"></d-cite><d-cite key="Omalu2"></d-cite>
- Work was dismissed and silenced by the NFL
- Still very much an issue, and currently it can only be diagnosed after death
- Boston University has an [awesome academic center](https://www.bu.edu/cte/) dedicated to CTE research

##### Measuring CTE Risk as an Occupational Risk
- NFL tries to downplay the impact or outright deny the existence of CTE
- The NFL doesn't want to deal with CTE and they try to introduce initiative that help but they're kinda lame
- In occupational health, typically for workers in factories working with potentially dangerous chemicals, you want to measure the risk associated with exposure
- In our case, the exposure is to repeated subconcussive and concussive head trauma
- When measuring risk, a typical approach would be to measure cumulative exposure and then look at outcomes
- This approach would systematically underestimate the risk associated with it
- You have a healthy worker survivor bias, where underlying resilience impacts which players even receive high exposure

- Work has been for the NBA showing that higher minute loads are riskier than a naive analysis would show, giving more credence to load management decisions </d-cite><d-cite key="nbaInjuries"></d-cite>

- FIND LITERATURE ON THE IMPACT OF SUBCONCUSSIVE IMPACTS

##### Modeling Subconcussive Strikes
- First going to demonstrate the phenomenon mathematically with few time points
- Then demonstrate it through simulation
- Present the very simplified model
  - No competing risks
  - Ignores play style or position
  - Difficult to measure prior exposure
  - Assume effect of a hit is the same over time (one might become more vulnerable as they take more hits)
- Some literature on accumulated exposure<d-cite key="cte1"></d-cite><d-cite key="cte2"></d-cite><d-cite key="cte3"></d-cite><d-cite key="cte4"></d-cite>
  - Difficult to measure the intensity of each exposure (watching tape, accelerometers in helmet, mouthguards)
  - Brain imaging pre/post sometimes
- Try to inform a simple exposure model using literature
