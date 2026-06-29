---
layout: distill
title: Failed Ideas
description: A running list, with descriptions, of ideas I had for research that ultimately fell flat (and why).
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

Most of the ideas I have don't turn out to be worth pursuing, but that doesn't mean good work wasn't done! I'm going to be putting as many of these failed ideas as I can in this post, with the hope that it is a useful resource to others. If you're reading something and think I made a mistake or believe there is a way to overcome the roadblock that stopped me, I would be delighted to hear about it in the comments.

## A Natural Experimental Design for Efficient Shapley Value Computation
Over the summer I chatted with [Professor Luca de Alfaro](https://luca.dealfaro.com/bio.html) a few times about research, and one of the topics was related to Shapley values. Additionally, I'm working as a data scientist with the [Center for Motivation and Change: Foundation for Change](https://cmcffc.org/), a nonprofit related to therapy and substance abuse. The nonprofit offers trainings in their evidence-based techniques, and the trainings go for a handful of weeks. Surveys are administered before beginning the training, as well as at the end. 

A question we could be interested in answering is how each week contributes to the overall learning of clients. One might opt for hierarchical linear modeling approaches or panel designs, but I thought that Shapley values might be a possible approach. By treating each week of the training as a player in a cooperative game, you can estimate the contribution of each week to overall learning by considering coalitions. This sort of setup, with a series of sessions in which learning or growth is the goal, occurs frequently. Corporate trainings, school, or skills-based therapies such as cognitive behavioral therapy are common examples. Coalitions naturally arise due to people missing sessions. While it would require some investigation, I don't think it's entirely implausible that absences would be completely at random ([MCAR](https://www.ncbi.nlm.nih.gov/books/NBK493614/))<d-cite key="mcar"></d-cite> or close enough to completely at random to make the method useful in many settings.

In practice, Shapley values are difficult to estimate because they require considering all $2^n$ coalitions for a game that has $n$ players. For a game with value function $v$ and set of players $N$, the Shapley value for player $i$ is defined as

$$
\varphi_i(v) = \sum_{S\subseteq N \setminus \{i\}} \frac{\vert S \vert ! (n - \vert S \vert - 1)!}{n!}[v(S \cup \{i\}) - v(S)] = \frac{1}{n}\sum_{S\subseteq N \setminus \{i\}} \binom{n-1}{\vert S \vert}^{-1}[v(S \cup \{i\}) - v(S)].
$$

In our case, the exponential number of coalitions is particularly distressing due to the small sample size of the surveys. This would lead to Shapley value estimates with considerable variance. Additionally, Shapley values don't naturally consider ordering when distinguishing between coalitions. Now, there has been work on modifications to Shapley values that consider orderings or players <d-cite key="orderedShap1"></d-cite><d-cite key="orderedShap2"></d-cite><d-cite key="orderedShap3"></d-cite>, but considering the ordering simply results in a further increase in the number of coalitions. 

In the setting of trainings however, each coalition can only occur in one order, since the trainings are offered in successive weeks. Furthermore, a participant is typically not allowed to miss as many sessions as they would like. An organizer may inform pariticipants that the outset that they are not allowed to miss more than $k$ sessions or they are removed. This is a very natural thing to do, as those who do not attend enough sessions are likely to miss out on synergistic elements across weeks and not properly represent learning. Again, I assumed missingness completely at random. 

With these observations, I decided to restrict the coalitions used to compute Shapley values to only those for which less than $k$ sessions missed. Now, the number of coalitions to consider *polynomial* in $k$ and $n$! In the Shapley value formula there is a scaling constant to satisfy the axioms, and I was unsure what it would be for mine, so I denoted it as $c$. Then, we will compute our modified Shapley values as

$$
\psi_i(v) = \sum_{S \subseteq N \setminus \{i\},\vert S \vert \geq n-k} c[v(S \cup \{i\}) - v(S)].
$$

Now on to attempting to prove the axioms for the Shapley values. The first axiom is **efficiency**, that 

$$
\sum_i \psi_i(v) = v(N).
$$

This is where things break down. For Shapley values, the easiest way to see efficiency is observe that the sum of Shapley values ends up being a telescoping sum, leaving $v(N) - v(\emptyset)$, which just ends up as $v(N)$. Unfortunately, by restricting the coalitions to only those above a certain size, the sum no longer telescopes, meaning there is no efficiency.

At this point, I decided that the idea was no longer worth pursuing. To me, efficiency is a fundamental property of the Shapley value and what makes it so desirable.

## Linear Algebra and SAT

In my undergraduate thesis, I spent a long time trying to encode the Nonogram puzzle in CNF. Following <d-cite key="minesweeper"></d-cite>, I tried to iterate over each constraint, and for each constraint enumerate all possible fillings as a DNF formula. They can then convert this into CNF. This approach works wonderfully for Minesweeper, but fails miserably for Nonogram. The reason is that the number of cells in each constraint (the neighborhood) is fixed in Minesweeper but grows with the size of the board $n$, for Nonogram. With this, in Minesweeper you can enumerate all possible fillings for each number that you might see on a cell, and convert that to CNF with only a few possibilities to consider, ever. For Nonogram, the possible constraints depends on $n$, and the number of fillings for a given constraint depends on $n$ as well. You end up with an exponential number of possible constraints and each has an exponential number of solutions, so enumerating all solutions is difficult (although feasible through dynamic programming). The real backbreaker is converting this DNF that has size exponential in $n$ into CNF, risking another exponential blowup in size. 

I implemented a branch-and-bound approach that would eliminate tautological clauses (clauses containing a literal and its negation) as well as subsumed clauses on the fly, but this still proved too slow. Any post-conversion cleaning did not prove effective, as my C program simply ran out of memory.

Ultimately I tried a different strategy to encode Nonogram by leveraging the similarity of its constraints to regular expressions which proved decently effective, but I've always been annoyed by how I was unable to apply the simple encoding strategy that was so effective for Minesweeper. While this post is not about how I ultimately got that encoding strategy to work, I was thinking about how to efficiently detect subsumption on a bike ride home from work and thought that implementing it through matrix operations might be a good route to try.

My intuition was that for two clauses, if we represent them as binary vectors to indicate which literals they contain (positive and negative occurences of a variable are different entries), you would know that the smaller subsumes the larger if the larger can be "projected" onto the smaller one in some sense. More precisely, for two binary vectors $\vec{a}$ and $\vec{b}$, if $\vec{a}\cdot\vec{b} = min(\lVert\vec{a}\rVert,\lVert\vec{b}\rVert)$. Note that the dot product can't be greater than $min(\lVert\vec{a}\rVert,\lVert\vec{b}\rVert)$, and if it is less that means that there is a literal in the smaller clause that is not contained in the larger one, meaning no subsumption.

The next task is to compute this efficiently. For a given CNF formula, the first step is to represent each clause as a binary vector. These binary vectors will then be stored in a matrix. I think that a data structure for CNF formulae would reasonably store the highest variable index and number of clauses, which give the dimensions of the matrix. In the Nonogram case, the highest variable index is $n$ which is *much* less than the number of clauses we will have, giving us an incredibly tall matrix $A$. In the process of converting each of the clauses to binary vector representation, one could compute the magnitudes of the vectors by tracking how many one-indices are stored for each vector. Thus, I will assume that we have a vector with the magnitude of the $i$-th clause $c_i$ in binary representation as the $i$-th element.

To compute the dot products between clauses, we simply compute $AA^T$. Then, for entry $A_{ij}$, we know that $c_i$ subsumes $c_j$ if 
$A_{ij} = min(\lVert\vec{c}_i\rVert,\lVert\vec{c}_j\rVert)$. We can gain further efficiency improvements by storing the magnitude vector in sorted order and then processing the smallest vectors first, thus removing as many future comparisons as possible.

So far, the idea is fine. It occured to me that if one can summarize the matrix in a low-dimensional space, that has the intuitive feel that the SAT instance is not that hard. I wanted to explore this using singular value decomposition (SVD), which attmpts to deconstruct our matrix $A$ into the product of three matrices as $A = U\Sigma V^T$. The real matrix of interest for us if $\Sigma$, which is a diagonal matrix with the singular values of $A$ on the diagonal. The square of these singular values give the eigenvalues, and each of these eigenvalues is the proportion of the variance in the original matrix that is explained by each of the components. In our case, since the SVD treats values in the original matrix as continuous, the new components that we create do not have any meaning logically (that I know of). What I wanted to explore is the relationship between number of components and proportion of variance explained for different formulas.

The idea falls apart because the SVD takes *much* longer to calculate than just solving the puzzle, at least on my local device. Improving the matrix construction process to be a sparse representation sped things up, but ultimately one would just be better off solving the puzzle.
