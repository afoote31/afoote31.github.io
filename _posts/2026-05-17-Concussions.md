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

A natural question that one studying CTE would like to answer is what the negative impact that repeated brain trauma has on NFL players, on average. Given that players cannot be randomized into different levels of head trauma, all we have to work with is observational data from games played. For this, we can turn to methods and approaches from the field of occupational epidemiology. Typically, occupational epidemiology is concerned with worker cohorts in settings like mines or factories with potentially dangerous chemicals where you want to measure the risk associated with exposure to those chemicals, but in our case the dangerous exposure is brain trauma, and the cohort is NFL players.

With only observational data, there are a variety of biases that must be considered. A full survey of potential biases can be found in <d-cite key="Grashow2019"></d-cite>, two of which are worth discussing here.

1. Improper Comparison Group

Without idealized randomization, the next best option is to find a natural comparison group that differs from the observed group by the variable of interest. Picking a proper comparison group can have an enormous effect on the estimated treatment effect. For instance, research has found that being a professional football player actually improves longevity <d-cite key="footballGood"></d-cite>. However, this work compares the longevity of the general US male population with NFL players. Clearly, NFL players differ from the general population in many ways, the most obvious being that professional athletes are in far better physical shape, potentially contributing to the observed difference in longevity. Some studies attempt to match using BMI, but this does not differentiate between fat and muscle mass<d-cite key="badComparison"></d-cite>. A much better comparison group was used in <d-cite key="footballGoodGood"></d-cite>, which took replacement players from a season in which the NFL players struck as the comparison group. Given that they were hired by NFL general managers, they were evaluated to be as close to matching in performance capacity to NFL players as possible, which makes it likely that they share many underlying physical traits with NFL players that would be exceedingly rare in the population. Importantly, they have minimal playing experience at the NFL level, allowing us to estimate the risk of brain trauma that comes from playing in the NFL. This paper found that a considerably increased risk of death for NFL players compared to replacement players, reversing the effect found when the general population was used as the comparison group.

2. Healthy Worker Survivor Bias

The healthy worker survivor bias has to do with who even gets measured for brain trauma in the population of interest. For a given exposure, some members of the cohort are more vulnerable to the ill effects than other members, even for the same fixed amount of exposure. The reason for this can be as simple as genetic variability. Thus, as exposure accumulates, some of the members of the cohort will be filtered out as they experience negative effects of the exposure. In this context, this could be a player retiring after a family member notices cognitive difficulties and pushes them to consider their health. With this, they will not accumulate any more brain trauma. Over time, this process will result in only the most naturally resilient cohort members accumulating the most exposure. This gradual selection will dampen the observed effect of the exposure, biasing the estimate towards the null hypothesis. In the extreme case, it can even show that the exposure is beneficial, a clearly nonsensical result.

Accounting for both of these 

Similar analyses have been conducted in the NBA, showing that higher minute loads are riskier than a naive analysis would show, giving more credence to load management decisions <d-cite key="nbaInjuries"></d-cite>. 


- NFL tries to downplay the impact or outright deny the existence of CTE
- The NFL doesn't want to deal with CTE and they try to introduce initiative that help but they're kinda lame
- In occupational health, typically for workers in factories working with 
- In our case, the exposure is to repeated subconcussive and concussive head trauma
- When measuring risk, a typical approach would be to measure cumulative exposure and then look at outcomes
- This approach would systematically underestimate the risk associated with it
- You have a healthy worker survivor bias, where underlying resilience impacts which players even receive high exposure

- Literature has shown that playing in the NFL improves longevity  but the methodology has been critiqued , particularly for not considering the healthy worker survivor bias

- Research using replacement players from an NFL strike (as opposed to the general population) as the comparison group found an increased risk of death over the course of the study for NFL players compared to replacement players , reversing the effect found from other studies

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
