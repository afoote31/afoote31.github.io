---
layout: distill
title: "Linear Algebra and SAT"
description: Two observations I had on how one might use linear algebra to process and analyze SAT instances. 
tags:
giscus_comments: true
date: 2026-02-28
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
I don't want to pretend that either of these ideas haven't been discovered by someone else before, but I found them interesting and they didn't come up immediately when I did a limited literature review. I would be excited to see papers that have developed these methods in a much richer manner than I have here!

### Subsumption with Matrix Operations
In my undergraduate thesis, I spent a long time trying to encode the Nonogram puzzle in CNF. Following <d-cite key="minesweeper"></d-cite>, I tried to iterate over each constraint, and for each constraint enumerate all possible fillings as a DNF formula. They can then convert this into CNF. This approach works wonderfully for Minesweeper, but fails miserably for Nonogram. The reason is that the number of cells in each constraint (the neighborhood) is fixed in Minesweeper but grows with the size of the board $n$, for Nonogram. With this, in Minesweeper you can enumerate all possible fillings for each number that you might see on a cell, and convert that to CNF with only a few possibilities to consider, ever. For Nonogram, the possible constraints depends on $n$, and the number of fillings for a given constraint depends on $n$ as well. You end up with an exponential number of possible constraints and each has an exponential number of solutions, so enumerating all solutions is difficult (although feasible through dynamic programming). The real backbreaker is converting this DNF that has size exponential in $n$ into CNF, risking another exponential blowup in size. 

I implemented a branch-and-bound approach that would eliminate tautological clauses (clauses containing a literal and its negation) as well as subsumed clauses on the fly, but this still proved too slow. Any post-conversion cleaning did not prove effective, as my C program simply ran out of memory.

Ultimately I tried a different strategy to encode Nonogram by leveraging the similarity of its constraints to regular expressions which proved decently effective, but I've always been annoyed by how I was unable to apply the simple encoding strategy that was so effective for Minesweeper. While this post is not about how I ultimately got that encoding strategy to work, I was thinking about how to efficiently detect subsumption on a bike ride home from work and thought that implementing it through matrix operations might be a good route to try.

My intuition was that for two clauses, if we represent them as binary vectors to indicate which literals they contain (positive and negative occurences of a variable are different entries), you would know that the smaller subsumes the larger if the larger can be "projected" onto the smaller one in some sense. More precisely, for two binary vectors $\vec{a}$ and $\vec{b}$, if $\vec{a}\cdot\vec{b} = min(\lVert\vec{a}\rVert,\lVert\vec{b}\rVert)$. Note that the dot product can't be greater than $min(\lVert\vec{a}\rVert,\lVert\vec{b}\rVert)$, and if it is less that means that there is a literal in the smaller clause that is not contained in the larger one, meaning no subsumption.

The next task is to compute this efficiently. For a given CNF formula, the first step is to represent each clause as a binary vector. These binary vectors will then be stored in a matrix. I think that a data structure for CNF formulae would reasonably store the highest variable index and number of clauses, which give the dimensions of the matrix. In the Nonogram case, the highest variable index is $n$ which is *much* less than the number of clauses we will have, giving us an incredibly tall matrix $A$. In the process of converting each of the clauses to binary vector representation, one could compute the magnitudes of the vectors by tracking how many one-indices are stored for each vector. Thus, I will assume that we have a vector with the magnitude of the $i$-th clause $c_i$ in binary representation as the $i$-th element.

To compute the dot products between clauses, we simply compute $AA^T$. Then, for entry $A_{ij}$, we know that $c_i$ subsumes $c_j$ if 
$A_{ij} = min(\lVert\vec{c}_i\rVert,\lVert\vec{c}_j\rVert)$. We can gain further efficiency improvements by storing the magnitude vector in sorted order and then processing the smallest vectors first, thus removing as many future comparisons as possible.

### SVD as a Heuristic for Difficulty

With the binary matrix representation in hand, I was wondering if there were any other possible ways to use it. It occured to me that if one can summarize the matrix in a low-dimensional space, that has the intuitive feel that the SAT instance is not that hard. I wanted to explore this using singular value decomposition (SVD), which attmpts to deconstruct our matrix $A$ into the product of three matrices as $A = U\Sigma V^T$. The real matrix of interest for us if $\Sigma$, which is a diagonal matrix with the singular values of $A$ on the diagonal. The square of these singular values give the eigenvalues, and each of these eigenvalues is the proportion of the variance in the original matrix that is explained by each of the components. In our case, since the SVD treats values in the original matrix as continuous, the new components that we create do not have any meaning logically (that I know of). What I want to explore is the relationship between number of components and proportion of variance explained for different formulas.

The SVD identifies the linear combinations of literals that account for the most variability in clauses. My intuition is that formulas that are easier to solve will end up having a smaller number of literal patterns repeated in clauses, and thus the formula will be summarized in fewer components than a more complex formula. As a side note, SVD is easiest to compute on matrices that are very tall. This applies directly to the use case of Nonogram encoding, as there are only a few variables but there is a large number of clauses.

To test this intuition, I will be doing some experiments using random 3-SAT instances to compare this new heuristic with some standard heuristics. Maybe the most common heuristic is the clause-to-variable ratio<d-cite key="randomSAT"></d-cite>. It has been shown that the difficulty of SAT instances spikes at a ratio of about 4.267 for random 3-SAT. For the analysis, I will consider formulas with 300 variables, and clause-to-variable ratios between 2 and 6. For each ratio, I will create 500 formulas by first sampling sets of three variables without replacement and then negating each with probability 0.5, repeating this process until the desired ratio between clauses and variables is met.

Once I've introduced the idea of dimensionality reduction or SVD for my representation, I will do some empirical comparisons of this approach to measure hardness compared to other approaches that already exist in literature. I'll take a bunch of SAT instances, compute the difficulty according to my metric (probably the number of dimensions to explain some proportion of the variance, which I can do a sensitivity analysis on), and plot that against the other metrics, looking for a correlation.
