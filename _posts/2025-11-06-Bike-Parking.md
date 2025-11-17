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

##### General Algorithm
From above, it looks like we need the expected costs from future racks in order to compute the cost of rack $i$. This is a textbook case of dynamic programming! In general, we have:

$$
V_i = \begin{cases}
    C                                                       & i = 0 \\
    \left(1-(1-p)^n\right)min(c_i,V_{i-1}) + (1-p)^nV_{i-1}     & \text{otherwise.}
\end{cases}
$$

Starting with the closest rack to the door ($i=1$), we can compute the expected cost of each rack in linear time. With those values in hand, we can now make a decision on where to park! Beginning at rack $r$ (the furthest from the seminar), decide the following at rack $i$:
1. If no spots, continue to rack $i-1$ and repeat.
2. Else:
    1. If $c_i < V_{i-1}$, park.
    2. Otherwise, continue to rack $i-1$.


### Unknown Values for $p$
The previous setup is not very realistic. I believe that it is reasonable to assume biking happens at random, but it is not reasonable to assume that the rider knows the probability $p$ of each spot being open. So, now let's consider the case when the rider must use an estimate $\hat{p}$. To estimate $p$, we can use the spots we've seen thus far, which are just Bernoulli trials with parameter $p$. Our estimator $\hat{p}$ will be the sample mean.

Our estimate introduces variance into the expected costs. If they become very noisy, it will be hard to know 

1. What do we want to measure here? I would like to be able to say things about the increase in expected error that results in not knowing the true probability $p$. Figure out precisely how to formulate this.



### Arriving to an Exam on Time
Minimizing the expected cost is a very natural thing to do, but certainly not the only. Imagine if you were racing to class, and an exam was going to start soon and you couldn't sit the exam if you arrived late. With a time $t$ until the exam starts and costs $c_i$ in terms of times, you want to find a rack that maximizes your probability of having cost less than $t$. Note that this may not result in you picking the same rack as the one that minimizes expected time. For instance, you might take a rack with a high cost just under $t$, even if, on average, you would be able to find a rack with lower cost by skipping the current rack.

I believe you just end up with a knapsack-like problem that you can also use dynamic programming on. I think that the incorporation of unknown/estimated $p$ could be interesting here.

### Allowing Circling Back

The rider always has the choice to turn back and return to a previously open spot. While this backtracking can be costly, it can also save time if the bike either overestimates the probability of open spots or ends up hitting a few unlucky racks in a row that are taken. To consider that, we have to incorporate information about the cost to travel between racks, as well as the openings seen thus far. I believe dynamic programming can still work here, as we're just developing a state space, but I haven't thought much about how to actually formulate it yet. I think that unknown/estimated $p$ will be interesting here.


### Limitations

I like to think that we have built up towards models of bike parking that are rich and decently realistic. However, they are all still built on the assumption that spots are filled randomly with equal probability. A very natural way to add complexity is to model the opening probabilities as a function of cost or rack index. That could make a lot of sense in settings where there is only one place people could be heading towards, so everyone has a similar objective (time or distance) and same priority.


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
- Large parking lots (Costco) or parking garages or maybe even emergency room
