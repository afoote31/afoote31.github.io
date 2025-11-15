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

**This post is still a work in progress. I hope you enjoy!**

### Introduction
I'm a resident of Palo Alto, and on Wednesdays I bike over to the Stanford campus to participate in the Department of Biomedical Data Science [Data Studio](https://dbds.stanford.edu/data-studio/). Stanford is an enormous, flat campus, so many traverse it via a bike. Since the seminar starts at 3pm, many of the bike racks are full or close to full as I arrive. This presents me with a decision to make: when should I continue biking towards the seminar, and at what point should I settle for an available spot that I come upon? 

#### Basic Setup
I'm going to start by describing the setup that I actually experience on my bike ride to work, where there are a few bike racks, and one cannot see the other racks when passing by one.

To state it somewhat more formally, there are $r$ bike racks, each of which has a cost $c_i$ associated with parking there. For simplicity, we will start by assuming that all racks have $n$ slots on them, potentially with some filled. Let $c$ be the cost that is incurred if you arrive at the door to the seminar without having found a parking spot. Our first goal will be to minimize the expected cost incurred when parking. To say anything about decisions, however, we need to say something about the parking process for the other bikes. Again, to start simple, we will assume that people park randomly. Honestly, I don't think that this is a particularly bad assumption. Even though I'm going to one building for the seminar, there are many other buildings that people might be going to, which would put different costs on each rack. Additionally, people might have different valuations of racks, and the combination of all of these policies might wash out to little better than random guessing anyways. So, each spot on each rack will be open with probability $p$. 

Just as a note, rather than assigning a cost $c$ to reaching the door without parking, we could pick some tolerance $\epsilon$ that dictates the probability of reaching the door that the rider is willing to take on. I like this setup better I think.

To build some intuition, let's consider the cases of one, and two racks.

##### One Rack
Let the size of the rack be $n_1$. If there is no spot open, I'm out of luck and just lose. If there is a spot open, we might have a decision to make. If we don't take the spot at this rack we will reach the door having not parked with probability one. So, if $\epsilon = 1$, we can go either way. Otherwise we have to park.

#### Two Racks
It gets more interesting here. 


### Adding Complexity
The previous setup is not very realistic. I believe that it is reasonable to assume biking happens at random, but it is not reasonable to assume that the rider knows the probability $p$ of each spot being open. Additionally, 


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
