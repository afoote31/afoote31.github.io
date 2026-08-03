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

American football is an inherently violent sport. Athletes wear extensive padding on their thighs, chest, and shoulders, and are required to wear a helmet. Prior research has found an average of 172 hamstring strains per year, with over half coming in the preseason and early regular season <d-cite key="hamstrings"></d-cite>, around 50 ACL tears each season <d-cite key="ACLs"></d-cite>, and many players play through injuries that would put us normal people out of commission for weeks. Sports medicine has made enormous strides over the years, with injuries that would formerly end careers (ACL and Achilles tears) now being setbacks that can usually be recovered from in a year or less.

A class of injury that is much more difficult to diagnose and treat is brain injuries. For years, the NFL highlighted violent collisions as a core entertainment aspect, with segments such as [Jacked Up](https://www.youtube.com/watch?v=3VxxmVr2GFw) celebrating helmet-to-helmet hits. Science has shown that these hits lead to concussions, a bouncing of the brain inside of the skull. For years, the NFL denied that concussions have any long-term negative health impacts, but Dr. Bennet Omalu proved otherwise in his analysis of NFL players' brains<d-cite key="Omalu1"></d-cite><d-cite key="Omalu2"></d-cite>. He showed that repeated sub-concussive impacts can also create lasting damage to the brain, contributing to a variety of mental health, neurodegenerative, and physical ailments. Today, Boston University has an [awesome academic center](https://www.bu.edu/cte/) dedicated to CTE research.

##### Measuring CTE Risk as an Occupational Risk
- NFL tries to downplay the impact or outright deny the existence of CTE
- The NFL doesn't want to deal with CTE and they try to introduce initiative that help but they're kinda lame
- In occupational health, typically for workers in factories working with potentially dangerous chemicals, you want to measure the risk associated with exposure
- In our case, the exposure is to repeated subconcussive and concussive head trauma
- When measuring risk, a typical approach would be to measure cumulative exposure and then look at outcomes
- This approach would systematically underestimate the risk associated with it
- You have a healthy worker survivor bias, where underlying resilience impacts which players even receive high exposure

- Work has been for the NBA showing that higher minute loads are riskier than a naive analysis would show, giving more credence to load management decisions <d-cite key="nbaInjuries"></d-cite>

- Literature has shown that playing in the NFL improves longevity <d-cite key="footballGood"></d-cite> but the methodology has been critiqued <d-cite key="Grashow2019"></d-cite>, particularly for not considering the healthy worker survivor bias

- Research using replacement players from an NFL strike (as opposed to the general population) as the comparison group found an increased risk of death over the course of the study for NFL players compared to replacement players <d-cite key="footballGoodGood"></d-cite>, reversing the effect found from other studies

- Other work shows that after accounting for selection bias, college/NFL players are 2.38 times as likely to suffer from CTE as high school players <d-cite key="cte5"></d-cite>

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
