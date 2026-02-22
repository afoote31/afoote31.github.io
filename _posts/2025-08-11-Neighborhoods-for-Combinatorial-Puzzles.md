---
layout: distill
title: Quarterback Evaluation as a Discrete Choice Model
description: I propose an approach to evaluating quarterback decision making
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

**THIS POST IS ONLY IN ITS INFANCY**

We want to evaluate quarterbacks as passers. Ideally, on each drive, they would maximize the expected value of the drive. On each passing play, they are presented with options of who to throw to, and a scout wants to know if they consistently choose the right person to throw to. There are ways to model choices, but first we need to judge the quarterback we first have to estimate the value of each option. 

### Estimating the Utility of Options

For this post, although it simplifies things considerably, we will assume that a quarterback is trying to maximize yards gained on each play. There are game scenarios where this is not the case (final two minutes of a half or when blowing the other team out) so data from those scenarios will be removed during modeling. I think this is a fine proxy to start, and it decreases the modeling complexity considerably by removing context. Furthermore, other works demonstrate that the sample size of the tracking data is not so big due to dependence among observations and correlated outcomes<d-cite key="fractionalTackles"></d-cite>, thus the data may not even have the complexity to handle an outcome variable such as expected points added anyways. Thus, for each option the quarterback has on a given play, we want to calculate their utility as the expected yards gained. This yards gained is a combination of air yards and yards after the catch. There will end up being lots of models to fit, so we're going to have a pretty simple YAC model. For the air yards portion, the quarterback only sees the part before the throw, so we have to predict how many additional yards will be gained while the ball is in the air. Again, this should be a pretty simple model. The air yards portion also has a completion probability component, so we have to fit that too. Note that we have selection bias if we fit a naive completion proabability model, as the receivers for which we have outcomes (complete/incomplete) are not a representative sample of all receivers who *could* be targeted. In order to handle this, I'm going to use inverse probability weighting, where we weight each observation that has an outcome by the inverse of the probability of receiving treatment (being targeted). In this way, observations with outcomes which have low probability of receiving treatment at all are considered more heavily when fitting the completion probability model. This combats selection bias and increases the generalizability of the completion probability model to untargeted players, for whom we still need utilities.


**Models to fit:**
- YAC model
- Air yards model
- Completion probability model
- Target probability model
- As the very final model, we fit the DCM

