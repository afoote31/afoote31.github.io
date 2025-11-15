---
layout: distill
title: Where to Park Your Bike
description: How to optimize your bike parking
tags:
giscus_comments: true
date: 2025-11-06
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

#### Introduction
I'm a resident of Palo Alto, and on Wednesdays I bike over to the Stanford campus to participate in the Department of Biomedical Data Science [Data Studio](https://dbds.stanford.edu/data-studio/). Stanford is an enormous, flat campus, so many traverse it via a bike. Since the seminar starts at 3pm, many of the bike racks are full or close to full as I arrive. This presents me with a decision to make: when should I continue biking towards the seminar, and at what point should I settle for an available spot that I come upon? During my journeys to and from the seminar, I've been thinking about this problem, and considering different framings of the problem to help me park as close as I can to the seminar.

#### Setup
To optimize the decision, we have to make some assumptions about the behavior of other bikers, decide how we want to value each parking spot, and define the bike rack setup. For starters, there is a cost to arriving at the entrance to the seminar and still be riding the bike. This happens if all spots are passed or all are taken. We will call this cost $C$. Then, whenever we consider an algorithm, it will weigh the probability of reaching the seminar without parking in the process 


I'm thinking that we might just frame the problem as a matter of risk tolerance, where we compute the probability of reaching the door

- Biking is everywhere on Stanford campus
- Lots of bike racks
- Naturally you want to park close to the building you will end up in
- Want to avoid getting to the building without finding a parking spot and then circling back
- Setups for the problem
  * Different cost functions (linear, squared)
  * Blocks of racks, visibility
- A few simple algorithms
- Analysis
- Probability components
- Large parking lots or parking garages or maybe even emergency room
