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
    affiliations:
      name: UC Berkeley
giscus_comments: true
bibliography: 2018-12-22-distill.bib

---

In this post, I explore the healthy worker survivor effect and methods to account for it through simulation. I use CTE in the NFL as an example of an exposure for which it is easy to underestimate the risk.

American football is an inherently violent sport. Athletes wear extensive padding on their thighs, chest, and shoulders, and are required to wear a helmet. Prior research has found an average of 172 hamstring strains per year<d-cite key="hamstrings"></d-cite> and around 50 ACL tears each season<d-cite key="ACLs"></d-cite>, with many players play through injuries that would put us normal people out of commission for weeks. Sports medicine has made enormous strides over the years, with injuries that would formerly end careers (ACL and Achilles tears) now being setbacks that can usually be recovered from in a year or less. Brain injuries are much more difficult to diagnose and treat. 

For years, the NFL highlighted violent collisions, with segments such as [Jacked Up](https://www.youtube.com/watch?v=3VxxmVr2GFw) celebrating helmet-to-helmet hits. Science has shown that these hits lead to concussions, a bouncing of the brain inside of the skull. For years, the NFL denied that concussions had any long-term negative health impacts, but Dr. Bennet Omalu proved otherwise in his analysis of NFL players' brains<d-cite key="Omalu1"></d-cite><d-cite key="Omalu2"></d-cite>. He showed that repeated sub-concussive impacts can also create lasting damage to the brain, contributing to a variety of mental health, neurodegenerative, and physical ailments. Today, Boston University has an [awesome academic center](https://www.bu.edu/cte/) dedicated to CTE research.

### Measuring CTE Risk as an Occupational Risk

A natural question that one studying CTE would like to answer is what the negative impact that repeated brain trauma has on NFL players, on average. Currently, CTE can only be officially diagnosed after death. However, innovations in monitoring devices and brain modeling have improved our ability to collect data on impacts to the brain as they occur<d-cite key="monitorAndModel"></d-cite>. Given that players cannot be randomized into different levels of head trauma, all we have to work with is observational data. For this, we can turn to methods and approaches from the field of occupational epidemiology. Typically, occupational epidemiology is concerned with worker cohorts in mines or factories and dangerous chemical exposures, but in our case the dangerous exposure is concussive collisions, and the cohort is NFL players.

In an observational data context, there are a variety of biases that must be considered. A full survey of potential biases can be found in <d-cite key="Grashow2019"></d-cite>, two of which I review here.

  1. Improper Comparison Group
     Without idealized randomization, the next best option is to find a natural comparison group that differs from the observed group only by the variable of interest. Picking a proper comparison group can have an enormous effect on the estimated treatment effect. For instance, research has found that being a professional football player actually improves longevity <d-cite key="footballGood"></d-cite>. However, this work compares the longevity of the general US male population with NFL players. Clearly, NFL players differ from the general population in many ways, the most obvious being that professional athletes are in far better physical shape, potentially contributing to the observed difference in longevity. Some studies attempt to match using BMI, but this does not differentiate between fat and muscle mass<d-cite key="badComparison"></d-cite>. A much better comparison group was used in <d-cite key="footballGoodGood"></d-cite>, which took replacement players from a season in which the NFL players struck as the comparison group. Given that they were hired by NFL general managers, they were evaluated to be as close to matching in performance capacity to NFL players as possible, which makes it likely that they share many underlying physical traits with NFL players that would be extremely rare in the general population. Importantly, they have minimal playing experience at the NFL level, allowing us to estimate the risk of brain trauma that comes from playing in the NFL. This paper found a considerably increased risk of death for NFL players compared to replacement players, reversing the effect found when the general population was used as the comparison group.
     2. Healthy Worker Survivor Bias
The healthy worker survivor bias has to do with who even gets measured for brain trauma in the population of interest. For a given exposure, some members of the cohort are more vulnerable to the ill effects than other members for the same fixed amount of exposure. The reason for this can be as simple as genetic variability. Thus, as exposure accumulates, some of the members of the cohort will be filtered out as they experience negative effects of the exposure. In this context, this could be a player retiring after a family member notices cognitive difficulties and pushes them to consider their health. Over time, only the most naturally resilient cohort members accumulate the most exposure. This gradual selection will dampen the observed effect of the exposure, biasing the estimate towards the null hypothesis. In the extreme case, it can even show that the exposure is beneficial.

Accounting for both of these sources of bias is *essential* in order to reliably estimate the risk of exposures. After accounting for selection bias, college/NFL players are 2.38 times as likely to suffer from CTE as high school players <d-cite key="cte5"></d-cite>. Similar analyses have been conducted in the NBA, showing that higher minute loads are riskier than a naive analysis would show, giving more credence to load management decisions <d-cite key="nbaInjuries"></d-cite>. 

In the rest of this post I will demonstrate just how damaging the application of naive methods can be through simulation. With this, I hope that others can identify settings in which similar biases occur in their work and use this post to improve their understanding of methods to control for these biases.


### Simulation Study

#### Setup
We'll be working with a cohort of 500 players, and each will have an initial vulnerability to concussions $v$, used as a multiplicative factor by which cumulated brain trauma is multiplied. Although concussions that remove a player from competition are more frequently discussed, head impacts occur on a spectrum, and subconcussive impacts are an essential part to understanding the risks involved with playing football<d-cite key="cte1"></d-cite><d-cite key="cte2"></d-cite><d-cite key="cte3"></d-cite><d-cite key="cte4"></d-cite>. Each player has around 800 plays per season, giving them 800 chances for an impact. I set the probability of an impact to be 0.025. The accumulated damage from one season is simulated from a Tweedie distribution, which naturally combines the binomial nature of impacts with continuous Gamma-distributed possible brain damage for each impact. I've included code to replicate my simulation study [here](https://github.com/afoote31/blog-post-code).

Prior to entering the NFL, players have typically played youth, high school, and college football. Thus, each comes in with prior damage accumulated. To model this, I give each player six seasons worth of damage (multiplied by their vulnerability) at time 0.

$$
v_i \sim N(1,0.05)
$$

$$
d_{i,0} \sim v_i \ast Tw(\mu = 144,\phi = 0.171,p = 14/9)
$$

$$
d_{i,t} = d_{i,t-1} + v_i\ast Tw(\mu = 24,\phi = 0.462,p = 14/9)
$$

As players accumulate damage, they are more likely to retire. In order to maintain positivity, we use a simple logistic probabilistic model to determine dropout probability. Combined with our damage generating process, we can simulate both the damage accumulated by players if they never retired along with the cohort that results from selection.

$$
\beta_0 = -10
$$

$$
\beta_1 = 0.05
$$

$$
\mathbb{P}(\text{Retire after season t}) = \frac{1}{1 + exp(-\beta_1 L_{t-1} - \beta_0)}
$$

#### Results

To demonstrate how the selection process filters out the players most likely to sustain more damage, I've plotted the average vulnerability in each of the seasons. Prior to any NFL play, the average vulnerability is one. However, as the seasons go on, the more resilient players tend to stick around. Additionally, the rate at which the average vulnerability drops increases over time. Another way to look at it is to examine observed versus true damage that would have occurred if the selection mechanism had not removed players from the cohort. Clearly, as the seasons go on, the damage that would have occurred if players had not retired outpaces the damage that is observed due to the selection for resilient players.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/avgV.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/avgD.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

If we would like to estimate the average brain damage accumulated after playing in the NFL for six seasons, the naive estimate would take the average of the damage accumulated by the players after six seasons. As we've established, this gives a biased underestimate. Since we've simulated the data, we know precisely how much bias there is relative to our ground truth estimate, which takes the average damage accumulated by all players *if they had played six seasons* with no retirement mechanism. Below we see that the HWSE if biasing our estimates considerably.

|   Method       | Estimate  | Bias      | Percent Bias   |
|   :---------:  | :--:      | :-------: | :------:       |
| Truth          | 289       |   0       | 0              |
| Survivors      | 249       |   -39.4   | -13.6          |


Modeling the healthy worker survivor effect is a bit tricky, as traditional regression fails. Consider the DAG below for just two time points, depicting causal relationships with arrows. The variables $A_0$ and $A_1$ are binary indicators of exposure (playing football), $L_1$ is damage accumulated after $A_0$, and $Y$ is total accumulated exposure after all possible treatments. We want to know the average brain trauma accumulated if a player were to play all seasons $(A_0 = 1, A_1 = 1)$. Traditional regression conditions on variables, asking questions of the form "among people who ended up with the exact same intermediate score $L_1 = 297$, what is the association between exposure $A_0$ and outcome $Y$?". What we really want to do is fix a treatment regime and estimate an outcome, i.e., "If we force everyone to take treatment $A_0 = 1$ and $A_1 = 1$, what continuous values of $L_1$ would they naturally develop, and what final outcome $Y$ would those dynamic $L_1$ values produce?".

With a traditional regression approach, we are in a pickle whether or not we include $L_1$ in the model. If you leave it out, we are omitting a variable that has an impact on the outcome $Y$ as well as our treatment $A_1$, introducing confounding. However, if we are to condition on $L_1$, we create a collider bias, where a spurious association between prior treatment $A_0$ and unobserved vulnerability $U$ muddies the estimate of the effect of $A_0$, as $U$ is also causally linked with $Y$. So either way you cannot isolate the causal effect of interest.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/DAG.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

The g-formula fixes exposures rather than variables, simulating to allow for flexibility. The steps are:

1. Fit a model to predict $L_1$ from baseline treatment $A_0$ using observed data.
2. Fit a model using observed data to predict $Y$ from $(A_0, L_1, A_1)$.
3. Simulate the cohort under the desired intervention $(A_0 = 1, A_1 = 1)$.
4. With this simulated dataset, generate new values $L_1^\ast$ using the model fit in step 1. This allows $L_1$ to experience the full variability from $A_0 = 1$, rather than fixing it.
5. Generate final $Y^\ast$ by first setting $A_1 = 1$ for everyone and then use the model from step 2 along with the simulated $L_1^\ast$ values.
6. The estimated outcome from policy $(A_0 = 1, A_1 = 1)$ is then just $\bar{Y}^\ast$.

This method seems sort of magical to me, and very unintuitive. Here is my understanding of how g-formula gets around the roadblocks from before. In standard regression, by conditioning on $L_1$, you fix its value, preventing changes in $A_0$ from pushing it up or down and preventing the indirect effect of $A_0$ on $Y$ through $L_1$ to be measured. The g-formula does not hold $L_1$ fixed. After you set the treatment in the simulation, you generate new values for $L_1$, allowing $A_0$ to impact $Y$ further up the chain. Additionally, the $L_1^\ast$ values are generated from a model that only depends on $A_0$, preventing the collider bias from occurring. I found both introductory papers<d-cite key="gMethodsIntro"></d-cite><d-cite key="gMethodsIntro2"></d-cite> and the original monograph<d-cite key="gMethodsIntro3"></d-cite> to be helpful in building my understanding.

Now to apply it! When applied to our simulated data, g-formula able to recover the true average damage accumulated, and is even resilient to model misspecification in this case. Additionally, by bootstrapping at the player level, we can construct valid confidence intervals, which end up being quite tight. The 95% confidence interval in this case ends up being 286 to 294.

|   Method       | Estimate  | Bias      | Percent Bias   |
|   :---------:  | :--:      | :-------: | :------:       |
| Truth          | 289       |   0       | 0              |
| Survivors      | 249       |   -39.4   | -13.6          |
| G-Formula      | 290       |   1.38    | 0.479          |


This post was meant to be an exploration of the healthy worker survivor bias and the methods that are typically used to resolve the bias. A major limitation of g-formula is its vulnerability to model misspecification. A suite of methods that is more flexible yet still highly rigorous is TMLE. The math behind those methods is mystifying to me, but I'm starting the biostatistics masters program at Berkeley in a week or two, and I'm excited to learn more about TMLE from the faculty who developed it! 



