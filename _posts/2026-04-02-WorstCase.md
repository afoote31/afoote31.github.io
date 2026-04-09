---
layout: distill
title: Worst-case Meta-analysis
date: 2026-04-02 13:48:00
featured: false
description: A summary of interesting papers on meta-analysis and modeling publication bias and p-hacking
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

WHAT IS AN IDEAL ESTIMATE IN THE RTMA AND MODEL PAPER!?!?!

Recently I had an itch to learn a bit about meta-analysis methods, so I dug through some papers to learn a bit about it. In this process, I stumbled onto a pair of papers by Professor [Maya Mathur](https://www.mayamathur.com/) at Stanford that I thought were very interesting.

#### Assessing robustness to worst case publication bias using a simple subset meta-analysis
In this paper<d-cite key="mathur2"></d-cite>, Mathur proposes an approach to meta-analysis that can be used in order to conduct of "worst case lower bound" sensitivity analysis. Rather than trying to estimate the strength of publication bias, a meta-analysis is conducted using only non-affirmative studies, which are those with non-significant P values
or point estimates in the undesired direction. This meta-analysis on non-affirmative studies approach (MAN) assumes worst-case publication bias where affirmative studies are infinitely more likely to be published than non-affirmative ones. Without knowing the true relative likelihoods of publication, MAN offers a conservative estimate by assuming the worst. To use MAN, you can use your favorite meta-analysis technique, but just on the non-affirmative studies. Thus, it is a complementary tool rather than a tool to replace other methods. If we find that results are still as we would hope under the worst-case publication bias, we can be optimistic that they will hold generally.

As a student with experience in algorithms research, I really liked this idea of a lower bound under minimal assumptions as a complement to any other method that might be used. I think that another real strength of the approach is its robustness to many typical limitations (heterogeneity, non-normal effects, small number of studies, or dependent effects). The paper contrasts this with funnel plots and statistical models. A funnel plot plots the point estimate on the horizontal axis and the standard error on the vertical axis. For smaller studies, you would expect to see greater variation in estimates, with the points creating a funnel shape. However, the spread in effects from small studies can come from real differences in those studies rather than publication bias, as some treatments may only be feasible to test on a small scale<d-cite key="funnel"></d-cite>. In addition to exploratory tools, there are methods that attempt to model the publication bias. It is shown in the paper that while these approaches can work, often times the model is misspecified and estimates become unreliable in the presence of p-hacking.

While there is no silver bullet, I really like the clean, intuitive, approach the MAN offers.

#### P-hacking in meta-analyses: A formalization and new meta-analytic methods
Having enjoyed the first paper, I dug into to another paper from Mathur that builds out a framework for p-hacking and publication bias more generally<d-cite key="mathur1"></d-cite>. I really like it as a model for these two related concepts, and think it could provide the tools to prove properties about meta-analysis methods in regards to these concepts.

##### Model
The mathematical of publication bias and p-hacking is probably my favorite part of the paper. They distinguish publication bias as selection *across* studies (SAS) where final estimates obtained by papers are selectively offered for review from p-hacking as selection *within* studies (SWS), where multiple estimates may be obtained within one study. Estimates in literature may be subject to either of these influences, or potentially both (a p-hacked estimate is selectively published). A basic model for meta-analysis without either SAS or SWS is 

$$
\hat{\theta}_i = \mu_i + \epsilon_i
$$

with $ \mu_i \sim \mathcal{N}(\mu , \tau^2) $ and $ \epsilon_i \sim \mathcal{N}(0,\sigma_i^2) $. Our study point estimates $ \hat{\theta}_i $ are centered on the study mean effect $\mu_i$, and these are normally distributed around the quantity of interest $\mu$, the overall mean population effect. The variances of the study point estimates are treated as fixed and known, while study effect variances are unknown.

An investigator in a potentially hacked study obtains multiple (possible correlated) estimates $\hat{\theta}^*_{i1}, \hat{\theta}^*\_{i2}, \dots $ but select a single "favored" estimate to report, yielding a favored estimate $\hat{\theta}\^*\_{iF}$. An estimate $\hat{\theta}\_{in}^* $ is affirmative, denoted $A\^*\_{in} = 1$, if 
$\frac{\hat{\theta}\_{in}\^*}{\sigma\^*\_i} > c $ for some critical value $c$. The paper proposes that hacked studies are hacked because the distribution of the study's ideal estimate differs from the distribution estimate, both marginally and conditional on the affirmative status of these two estimates. This implies that in unhacked studies, the probability that a favored estimate is affirmative is equal to the probability that the ideal estimate is affirmative. A hacked study ($H_i^* = 1$) is successful iff the favored estimate $\hat{\theta}\^*\_{iF}$ is affirmative (otherwise considered unsuccessful).


##### Right-Truncated Meta-Analysis (RTMA)

In the paper they just recommend doing some diagnostics including a QQ-plot for the Jeffrey's prior, but explore the topic through extensive simulation in a later paper<d-cite key="mathur3"></d-cite>.

##### Meta-Analysis of Non-Affirmative Studies (MAN)
