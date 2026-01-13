---
layout: distill
title: "23 Sacks in 17 Games: Contextualizing Myles Garrett's Record-Breaking Season"
description: With Myles Garrett breaking the official single season sack record, I explore how it compares to other all time great pass rush seasons. 
tags:
giscus_comments: true
date: 2026-1-06
featured: true
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

In the 2025 NFL regular season, Myles Garrett chasing the all time single season sack record was one of the main storylines. After a productive start to the season, Garrett cooled off between weeks three and seven, before exploding for 13 sacks in four weeks. After that, the race was on! This performance comes on the heels of him becoming (temporarily) the highest paid non-quarterback player in NFL history in the offseason, inking a contract worth 160 million dollars with 123 million in guaranteed money. However, it took him until the seventeenth game of the season to earn the record. This has led some critics to discredit the record as the byproduct of the extended season.

Putting this monumental achievement in the context of other all time seasons is difficult given the different play styles across eras. For instance, offenses have become considerably more pass-heavy over time, giving defenders more opportunities to sack the quarterback (see plot below). On the other hand, since Bill Walsh revolutionized football with the introduction of the west coast offense, first in Cincinnati under Paul Brown (1968-1975) and then as the architect of the 49ers dynasty, short passing has become more and more popular. This decreases the quality of the opportunities that pass rushers receive, as they have less time to get to the quarterback. In recent years, rich data sources such as those provided by the [Kaggle NFL Big Data Bowl](https://www.kaggle.com/competitions/nfl-big-data-bowl-2026-analytics) have allowed new stats to be developed that are better able to account for these nuances. However, the differences are still difficult to account for historically in seasons without tracking data. On top of all of this, sacks were not counted as an official statistic until 1982, leaving only unofficial counts for many Hall of Famers. In this post, I will be considering unofficial sack totals, which were tallied by football historian John Turney for [NFL Football Journal](https://nflfootballjournal.blogspot.com/). The question we want to answer is whether Garrett's achievement is in fact the result of more games, or if other players would have done similar or worse with the opportunities that Garrett received.


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/passingYards.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Average pass attempts per game in the NFL each season, with top sack seasons colored red.
</div>


The other players I will be considering are those that bettered Deacon Jones's 1967 season with 21.5 sacks, yielding seven players along with Jones. The players and their seasons are:

| Player            | Sack Total      | Season        | Games Played  |
| :-----------      | :------------:  |:------------: |:-------------:|
| Al Baker          | 23              | 1978          | 16            |
| Myles Garrett     | 23              | 2025          | 17            |
| Michael Strahan   | 22.5            | 2001          | 16            |
| TJ Watt           | 22.5            | 2021          | 15            |
| Jared Allen       | 22              | 2011          | 16            |
| Mark Gastineau    | 22              | 1984          | 16            |
| Justin Houston    | 22              | 2014          | 16            |
| Deacon Jones      | 22              | 1964          | 14            |
| Deacon Jones      | 22              | 1968          | 14            |
| Deacon Jones      | 21.5            | 1967          | 14            |

### The Greatness of Deacon Jones

Although the totals are unofficial, Deacon Jones's totals are truly incredible given that he only had 14 games in his seasons. Along with Gino Marchetti of the Colts, he was one of the first famous pass rushers in the NFL, playing 14 seasons from 1961 to 1974. Over his career, he played primarily for the Rams, forming the "Fearsome Foursome" alongside Rosey Grier, Lamar Lundy, and fellow Hall of Famer Merlin Olsen, which was lauded by Dick Butkus as "the most dominant line in football history". Additionally, Jones is widely credited with coining the term "sack". His explanation of the term:

> "Sacking the quarterback is just like you devastate a city or you cream a multitude of people. I mean, it's just like you put all the offensive players in one bag and I just take a baseball bat and beat on the bag." - Deacon Jones


### Comparing Players

Typically, to compare players across eras, the record books will note their progress at the previous number of games, e.g. including 16-game marks along with full 17-game season totals. However, those extra games did in fact happen, and the matchup being left out could just have well been the week 5 matchup, as this is decided by schedule makers. Thus, we can consider all 14 game subsets of a player's season to see the distribution of 14 game seasons that the player could have had given their performances in the 17 game season. The reason for 14 games is that this is the number that Deacon Jones played in his seasons, and there is no player from earlier eras (which had less than 14 games) in the top 100 season sack totals. This approach assumes that performances are independent week-to-week. One may argue that a coach has more information to game plan or would change their game plan based on previous performances. I would respond that the players on this list are known quantities, and are always considered as the most important part of an offensive gameplan. An offensive coordinator will not go easier or harder on any of these players based on their performances from the weeks prior.

For our analysis, for each player, we will compute all 14 game subsets of a player's per-game sack performance. For each of these 14-game seasons, we can compute their sack total. Then, we can compute the proportion of 14-game seasons in which the player match or better Jones's best seasons with 22 sacks. If a player only reaches 22 sacks in a small subset of seasons, that suggests their total is more dependent on having more games. I prefer this approach over using sacks-per-game for our analysis, as that approach would require an arbitrary volume cutoff to be established. Also, this approach allows us to see a distribution of potential performances rather than boiling each player down to just one number. Below are plots for each player, along with a table of proportions.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/AlBaker.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/MylesGarrett.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
  The distribution of sack totals for all 14 game subsets from the top sack seasons. Subsets with more than 22 sacks are highlighted in red.
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/TJWatt.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/JaredAllen.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
  The distribution of sack totals for all 14 game subsets from the top sack seasons. Subsets with more than 22 sacks are highlighted in red.
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/MarkGastineau.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/JustinHouston.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
  The distribution of sack totals for all 14 game subsets from the top sack seasons. Subsets with more than 22 sacks are highlighted in red.
</div>

| Player            | Proportion $\geq$ 22 Sacks  |
| :-----------      | :------------:              |
| Al Baker          | 0.292                       |
| Myles Garrett     | 0.074                       |
| Michael Strahan   | 0.075                       |
| TJ Watt           | 0.267                       |
| Jared Allen       | 0.025                       |
| Mark Gastineau    | 0.025                       |
| Justin Houston    | 0.025                       |


This analysis suggests that Myles Garrett's breaking of the record was a result of extra games, since he would have a very small likelihood of breaking the record if he only had 14 games to do it. On the other hand, Al Baker's 23 sacks in 1978 and TJ Watt's 22.5 in 2021 would have reached 22 sacks over a quarter of the time, which in my mind indicates a more impressive season, and a more reasonable claim at the record. However, there are only 15 possible 14 game subsets from TJ Watt's 2021 season, which introduces considerable variability (there are 120 for Baker). Thus, I would consider Baker's 23 sacks in 1978 to be more impressive than Garrett's 23 in 2025. All in all, Garrett had a phenomenal 2025 campaign, and for his effort he will join an elite list of repeat DPOY winners (Lawrence Taylor, JJ Watt, Aaron Donald, Joe Greene, Mike Singletary, Bruce Smith, Reggie White, Ray Lewis). If Garrett can put together a couple more elite seasons, he'll start to be mentioned in the pantheon of great pass rushers, and may even secure another DPOY award or two. Right now, however, Reggie White and Deacon Jones still reign supreme for me as the greatest pass rushers in NFL history.
