---
layout: distill
title: A Mathematical Argument Against Easy Exams
description: A thought experiment, using probability theory, on why exams should not be made easy.
tags:
giscus_comments: true
date: 2025-07-24
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

This analysis was inspired by a conversation I had about grades on a midterm exam in a large organic chemistry course. It was pointed out to me that when most students do well on an exam, their grades are clumped together near the top end of the possible scores. Then, even a small deviation in points can result in a large change in rank in the class, resulting in the student's grade in the course potential having considerably more volatility. If, on the other hand, the test was more difficult, one might expect to see the scores more spread out. With this, a small change in score would be less likely to result in a large shift in rank.

It got me thinking about how one might describe this mathematically. After all, this is really a question about comparing variability in the random events of test scores and class rankings. The model I present here is certainly a simplification of the real world, but I think it does a pretty good job of illustrating the concept.

Suppose we have a class of $s$ students, and each of them is given an exam with $n$ questions. We're going to make the following assumptions:

1. Each of the questions is equally difficult, thus each has a probability $p$ of being answered correctly.
2. Each of the students has the same probability $p$ of answering each question correctly.
3. The probabilities of answering the questions correctly are independent.
4. Each student's performance is independent of the others.

Let's review these assumptions. The first two certainly may not reflect reality. Exams usually include softballs to start and a handful of tricky questions at the end, and some students will simply be more knowledgeable about the topic than others. The third assumption is plausible, especially for larger cumulative exams where each question may cover a topic. Lastly, it is reasonable to assume that the performance of one student is independent of the performance of another, assuming they can't communicate during the exam.

Since an exam is just a sequence of $n$ independent trials with success probability $p$ on each trial, a random variable $\xi$ for a student's score is a binomial random variable, thus they will get $k$ questions correct with probability 

$$
\mathbb{P}(\xi = k) = \binom{n}{k}p^k(1-p)^{n-k}.
$$

Next, we want to describe probabilities related to the student's rank. For this, let's consider the probability that $r-1$ students get more than $k$ questions correct. Since we assumed that student scores are independent, we again have a binomial random variable setup! There are $s-1$ independent trials, where a success means that student answers more than $k$ questions correctly on the exam. This occurs with probability 

$$
\sum_{i=k+1}^n \binom{n}{i}p^i(1-p)^{n-i}.
$$

The probability that a student, answering $k$ questions correctly, has $r-1$ students perform better, is then

$$
\binom{s-1}{r-1}\left(\sum_{i=k+1}^n \binom{n}{i}p^i(1-p)^{n-i}\right)^{r-1}\left(1 - \sum_{i=k+1}^n \binom{n}{i}p^i(1-p)^{n-i}\right)^{s-r}.
$$

Taking a step back, we see that the score on an exam $\xi \sim Binom(n,p)$ and the rank of a student, conditional on answering $k$ questions correctly, follows a distribtion 

$$
1 + Binom(s-1,\sum_{i=k+1}^n \binom{n}{i}p^i(1-p)^{n-i}).
$$

Again, what we're really interested in here is comparing the variability in score and the variability in rank. Thus, next we will compute the variance of each. For convenience, we will take $q_k = \sum_{i=k+1}^n \binom{n}{i}p^i(1-p)^{n-i}$. The variance of $\xi$ is simple, it is just $np(1-p)$. For the rank, however, we only have the distribution conditional on the exam score, so we must use the law of total variance:

$$
V(Rank) = E\left[V(Rank \vert \xi = k)\right] + V\left(E\left[Rank \vert \xi = k\right]\right)
$$

Let's consider each of the elements of the sum individually.

$$
E\left[V(Rank \vert \xi = k)\right] = \sum_{k=0}^n \mathbb{P}(\xi = k)V(Rank \vert \xi = k) = \sum_{k=0}^n \binom{n}{k} p^k(1-p)^{n-k} \left[(s-1)q_k(1-q_k)\right]
$$

$$
\begin{align*}
V\left(E\left[Rank \vert \xi = k\right]\right) &= V(1 + (s-1)q_k) = (s-1)^2V(q_k) = (s-1)^2\left[E(q_k^2) - E(q_k)^2\right] \\
&= (s-1)^2\left[\sum_{k=0}^n\mathbb{P}(\xi = k)q_k^2 - \left(\sum_{k=0}^n \mathbb{P}(\xi=k)q_k\right)^2\right] \\
&= (s-1)^2\left[\sum_{k=0}^n\binom{n}{k}p^k(1-p)^{n-k}q_k^2 - \left(\sum_{k=0}^n \binom{n}{k}p^k(1-p)^{n-k} q_k\right)^2\right]
\end{align*}
$$

We end up with an ugly term for the variance that can probably be crunched down, but I don't explore that here. Instead, I want to explore how the two variances relate to one another. Below I will include sliders that allow the user to try out different values for $n$, $k$, and $s$ and from that see how the variability in a student's score relates to the variability in their rank. That is still to come...
