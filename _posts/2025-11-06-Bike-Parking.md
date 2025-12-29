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

I'm a resident of Palo Alto, and on Wednesdays I bike over to the Stanford campus to participate in the Department of Biomedical Data Science [Data Studio](https://dbds.stanford.edu/data-studio/). Stanford is an enormous, flat campus, so many traverse it via a bike. Since the seminar starts at 3pm, many of the bike racks are full or close to full as I arrive. This presents me with a decision to make: when should I continue biking towards the seminar, and at what point should I settle for an available spot that I come upon? 

### Basic Setup
I'm going to start by describing the setup that I actually experience on my bike ride to work, where there are a few bike racks, and one cannot see the other racks when passing by one.

To state it somewhat more formally, there are $r$ bike racks, each of which has a cost $c_i$ associated with parking there. For simplicity, we will start by assuming that all racks have $n$ slots on them, potentially with some filled. Let $C$ be the cost that is incurred if you arrive at the door to the seminar without having found a parking spot. Our first goal will be to minimize the expected cost incurred when parking. To say anything about decisions, however, we need to say something about the parking process for the other bikes. Again, to start simple, we will assume that people park randomly. Honestly, I don't think that this is a particularly bad assumption. Even though I'm going to one building for the seminar, there are many other buildings that people might be going to, which would put different costs on each rack. Additionally, people might have different valuations of racks, and the combination of all of these policies might wash out to little better than random guessing anyways. So, each spot on each rack will be open with probability $p$. For the sake of notation, 

$$
\rho = 1 - (1-p)^n
$$

will be the probability that a rack has an open spot. To build some intuition, let's consider the cases of zero, one, and two racks. We'll consider the expected cost, as well as the decision that a rider would make upon arriving at that rack.

##### Zero Racks
You have to incur cost $C$.

##### One Rack
When arriving at this rack, if there are no spots open, it is just the zero rack case. If there is a spot open, continue when $c_1 > C$, and park at rack one otherwise. The expected cost of the first rack is 

$$
V_1 = C(1-\rho) + min(C,c_1)\rho.
$$

##### Two Racks
When arriving at this rack, if there are no spots open, we have to go to the next rack, which has expected cost $V_1$. However, if there is an open spot, there is a decision to be made. One should take the spot when $c_2 < V_1$, meaning that the cost incurred by parking is less than what you would see on average by continuing. This yields an expected cost for the first rack of 

$$
V_2 = V_1(1-\rho) + min(V_1,c_2)\rho.
$$

##### General Algorithm
From above, it looks like we need the expected costs from future racks in order to compute the cost of rack $i$. This is a textbook case of dynamic programming! In general, we have:

$$
V_i = \begin{cases}
    C                                                       & i = 0 \\
    \rho min(c_i,V_{i-1}) + (1-\rho)V_{i-1}     & \text{otherwise.}
\end{cases}
$$

Starting with the closest rack to the door ($i=1$), we can compute the expected cost of each rack in linear time. With those values in hand, we can now make a decision on where to park! Beginning at rack $r$ (the furthest from the seminar), decide the following at rack $i$:
1. If no spots, continue to rack $i-1$ and repeat.
2. Else:
    1. If $c_i < V_{i-1}$, park.
    2. Otherwise, continue to rack $i-1$.

### Arriving to an Exam on Time
Minimizing the expected cost is a very natural thing to do, but certainly not the only way to frame the problem. Imagine if you were racing to class, and an exam was going to start soon and you couldn't sit the exam if you arrived late. Let the time budge be $t$ until the exam starts and costs $c_i$ in terms of times. Your goal now is to pick a rack that maximizes your probability of arriving on time. Note that this may not result in you picking the same rack as the one that minimizes expected time. For instance, you might take a rack with a high cost just under $t$, even if, on average, you would be able to find a rack with lower cost by skipping the current rack.

Under some assumptions that I believe are reasonable, we get a very simple greedy policy. As you arrive at each rack, see if $c_i \leq t$ and if the rack has an open spot. If so, park there, as parking there will yield a probability of one for arriving to the exam on time. If $c_i > t$, continue, as parking here has probability zero of arriving to the exam on time. If the rack is occupied, you must continue.

A key assumption for the greedy algorithm to work is that travel time between racks is negligible. Since biking is much faster than walking (especially when rushing to an exam), the cost of travel between racks would end up being negligible relative to the $c_i$.

### Allowing Circling Back

The rider always has the choice to turn back and return to a previously open spot. While this backtracking can be costly, it can also save time if the bike either overestimates the probability of open spots or ends up hitting a few unlucky racks in a row that are taken. To consider that, we have to incorporate information about the cost to travel between racks, as well as the openings seen thus far. We can still use relatively straight-forward dynamic programming here. We will assume that if we pass an open rack that rack remains open and we do not have to consider the probability of it being taken. Our objective is to minimize the cost incurred, on average.

Take $b_{ij}$ to be the cost to travel from rack $i$ to rack $j$, with the $b$ to emphasize that it is for backtracking. The costs will not be symmetric, meaning $b_{ij}$ doesn't necessarily equal $b_{ji}$ and $c_i$ doesn't necessarily equal the sum of $b_{ij}$ for $j$ between zero and $i$. Since time is the most natural cost here, this is sensible, as backtracking from rack $i$ to rack $j$ would require slowing down, turning around, and speeding up again, while traveling from rack $j$ to rack $i$ can be done with direct biking.

Intuitively, upon reaching rack $i$ and seeing it to be open, we can park, continue, or backtrack. If we continue, we should remember that this rack is open, as it will influence our calculation at later racks. If rack $i$ is closed, the choices are to continue or to backtrack, and we should note down that it is a closed rack for later calculations. This scenario still has a dynamic programming feel to it, but now the actions and values of a state depend on the index of the rack being observed as well as the set $S$ of racks observed to be open. Note that we have a Markov decision process on our hands, as the value at a state $(i,S)$ does not depend on any history, and the future depends only on the state and the actions taken.

The actions that can be taken in a state $(i,S)$ depend on whether rack $i$ is open or not. If the door is reached without parking, one can either incur the cost $C$ or backtrack. Next, if forward progress is still possible and rack $i$ is open, the options are to park, backtrack, or continue forward. In the case that forward progress is possible but parking is not, the options are only to backtrack or continue forward.

$$
\mathcal{A}(i,S) = 
\begin{cases}
\\{\text{Incur cost } C,\text{Backtrack to }j > i\\} & i = 0,j \in S,i \in S \\
\\{\text{Park},\text{Backtrack to }j > i, \text{Forward to }i-1 \\} & i > 0,j \in S, i \in S \\
\\{\text{Backtrack to }j > i, \text{Forward to }i-1 \\} & i > 0,j \in S, i \notin S \\
\end{cases}
$$

Upon parking, a terminal state is reached with cost $c_i$ for rack $i$ or $C$ if all racks are passed and backtracking not chosen. If the action chosen is backtracking to rack $j$, then the new state is $(j,S)$ with probability 1. Finally, if continuing forward is chosen, state $(i-1, S \cup \\{i-1\\})$ is reached with probability $\rho$ and state 
$(i-1, S)$ is reached with probability $1-\rho$. The value of a state, $V(i,S)$, defined as

$$
V(i,S) = min_{a \in \mathcal{A}(i,s)} Q(i,S,a)
$$

can be computed relatively easily, as the Q-values more or less fall right out from the discussion above.


$$
Q(i,S,\text{Park}) = c_i\\
$$

$$
Q(i,S,\text{Forward})  = \rho V(i-1, S \cup \\{i-1\\}) + (1-\rho)V(i-1, S)\\
$$

$$
Q(i,S,\text{Backtrack to }j) = V(j, S)\\
$$

Unfortunately, the number of states is exponential in the number of racks in the worst case, as there are funky policies that could put you in any rack position with any combination of open/closed racks. However, we often wouldn't see this in practice. Given a vector of costs $c_i$ and backtrack costs $b_{ij}$, one can use a branch-and-bound approach to enumerate the states, pruning out branches that only include options that would never be taken under the costs provided.

One way to make the computation more feasible is to impose constraints on $c_i$ and $b_{ij}$. It is natural to assume that parking at a rack seen earlier is more costly than parking at a later rack, and that backtracking further costs more, i.e., 

$$
c_i > c_{i-1}\\
$$

$$
b_{ij+1} > b_{ij}.\\
$$

With these assumptions, it would never make sense to backtrack, since a backtracking cost would be incurred just to park at a more costly rack! The inclusion of both monotonicity constraints reduces the problem to the first one we considered, but both of these monotonicity constraints seem natural to me.

### Limitations

I like to think that we have considered models of bike parking that are rich and decently realistic. However, they are all still built on the assumption that spots are filled randomly with equal probability. A very natural way to add complexity is to model the opening probabilities as a function of cost or rack index. That could make a lot of sense in settings where there is only one place people could be heading towards, so everyone has a similar objective (time or distance) and same priority. Additionally, a natural next step would be to estimate $p$ from observed parking, rather than taking it as a known quantity. One could then combine those two additional complexities as well. I hope to explore these possibilities in future posts, potentially extending this one.

Along with using this approach to understand bike parking, one could use it to model parking in large parking lots such as Costco or in parking garages, where there are multiple discrete parking options to observe (parking lot aisles for Costco or levels for a parking garage), and one must decide whether to park at an observed open spot or to continue to a more desirable location.
