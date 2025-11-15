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

**This post is still a work in progress.**

I'm a resident of Palo Alto, and on Wednesdays I bike over to the Stanford campus to participate in the Department of Biomedical Data Science [Data Studio](https://dbds.stanford.edu/data-studio/). Stanford is an enormous, flat campus, so many traverse it via a bike. Since the seminar starts at 3pm, many of the bike racks are full or close to full as I arrive. This presents me with a decision to make: when should I continue biking towards the seminar, and at what point should I settle for an available spot that I come upon? 

### Basic Setup
I'm going to start by describing the setup that I actually experience on my bike ride to work, where there are a few bike racks, and one cannot see the other racks when passing by one.

To state it somewhat more formally, there are $r$ bike racks, each of which has a cost $c_i$ associated with parking there. For simplicity, we will start by assuming that all racks have $n$ slots on them, potentially with some filled. Let $C$ be the cost that is incurred if you arrive at the door to the seminar without having found a parking spot. Our first goal will be to minimize the expected cost incurred when parking. To say anything about decisions, however, we need to say something about the parking process for the other bikes. Again, to start simple, we will assume that people park randomly. Honestly, I don't think that this is a particularly bad assumption. Even though I'm going to one building for the seminar, there are many other buildings that people might be going to, which would put different costs on each rack. Additionally, people might have different valuations of racks, and the combination of all of these policies might wash out to little better than random guessing anyways. So, each spot on each rack will be open with probability $p$.

To build some intuition, let's consider the cases of one, and two racks. We'll consider the expected cost, as well as the decision that a rider would make upon arriving at that rack.

##### Zero Racks
You have to incur cost $C$.

##### One Rack
When arriving at this rack, if there are no spots open, it is just the zero rack case. If there is a spot open, continue when $c_1 < C$, and park at rack one otherwise. The expected cost of the first rack is 
$$
V_1 = C(1 - p)^n + min(C,c_1)\left(1 - (1-p)^n\right).
$$

##### Two Racks
When arriving at this rack, if there are no spots open, we have to go to the next rack, which has expected cost $V_1$. However, if there is an open spot, there is a decision to be made. One should take the spot when $c_2 < V_1$, meaning that the cost incurred by parking is less than what you would see on average by continuing. This yields an expected cost for the first rack of 
$$
V_2 = V_1(1-p)^n + min(V_1,c_2)\left(1 - (1-p)^n\right).
$$

#### General Algorithm
From above, it looks like we need the expected costs from future racks in order to compute the cost of rack $i$. This is a textbook case of dynamic programming! In general, we have:

$$
V_i = \begin{cases}
    C                                                       & i = 0 \\
    \left(1-(1-p)^n\right)min(c_i,V_i-1) + (1-p)^nV_i-1     & \text{otherwise.}
\end{cases}
$$

Starting with the closest rack to the door ($i=1$), we can compute the expected cost of each rack in linear time. With those values in hand, we can now make a decision on where to park! Beginning at rack $r$ (the furthest from the seminar), decide the following at rack $i$:
1. If no spots, continue to rack $i-1$ and repeat.
2. Else:
    1. If $c_i < V_i-1$, park.
    2. Otherwise, continue to rack $i-1$.


### Adding Complexity
The previous setup is not very realistic. I believe that it is reasonable to assume biking happens at random, but it is not reasonable to assume that the rider knows the probability $p$ of each spot being open. So, now let's consider the case when the rider must use an estimate $\hat{p}$. A simple and intuitive way for a rider to estimate $p$ is to simply take the proportion of spots open from the spots that they have seen thus far. Let's see how this changes things.

1. What do we want to measure here? I would like to be able to say things about the increase in expected error that results in not knowing the true probability $p$. Figure out precisely how to formulate this.


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
