---
layout: distill
title: Myles Garrett Broke the Single Season Sack Record. So?
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

* Need to motivate Deacon Jones comparison better
* Include links to per-game sack counts for older players

In the 2025 NFL regular season, Myles Garrett chasing the all time single season sack record was one of the main storylines. After a productive start to the season, Garrett cooled off between weeks three and seven, before exploding for 13 sacks in four weeks. After that, the race was on! This performance comes on the heels of him becoming (temporarily) the highest paid non-quarterback player in NFL history in the offseason, inking a contract worth `$`160 million with `$`123 in guaranteed money. 

However, it took him until the seventeenth game of the season to earn the record. This has led some critics to discredit the record as the byproduct of more opportunities. Some even take issue with the way that Joe Burrow fell to the ground when pressured by Garrett, although it certainly doesn't have the same optics as the Strahan sack on Favre in 2001.

Putting this monumental achievement in the context of other all time seasons is difficult given the different play styles across eras. For instance, offenses have become considerably more pass-heavy over time, giving defenders more opportunities to sack the quarterback (see plot below). On the other hand, since Bill Walsh revolutionized football with the introduction of the west coast offense first in Cincinnati under Paul Brown (1968-1975) before architecting a dynasty with the 49ers using the scheme, short passing has become more and more popular. This decreases the quality of the opportunities that pass rushers receive, as they have less time to get to the quarterback. In recent years, rich data sources such as that provided by the [Kaggle NFL Big Data Bowl](https://www.kaggle.com/competitions/nfl-big-data-bowl-2026-analytics) have allowed new stats to be developed that are better able to account for these nuances. However, the differences are still difficult to account for historically, in seasons without tracking data. On top of all of this, sacks were not counted as an official statistic until 1982, leaving only unofficial counts for many Hall of Famers. In this post, I will be considering unofficial sack totals, which were tallied by football historian and John Turney for [NFL Football Journal](https://nflfootballjournal.blogspot.com/).


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/passingYards.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Average pass attempts per game in the NFL each season, with top sack seasons colored red.
</div>




For this post, we will be taking the sack totals at face value, admittedly a limitation. I will be considering the players that bettered Deacon Jones's 1967 season with 21.5 sacks, yielding seven players along with Jones. The players and their seasons are:

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

Although the totals are unofficial, Deacon Jones's totals are truly incredible given that he only had 14 games. Along with Gino Marchetti of the Colts, he was one of the first famous pass rushers in the NFL, playing 14 seasons from 1961 to 1974. Over his remarkably consistent 14 seasons, he played primarily for the Rams, forming the "Fearsome Foursome" alongside Rosey Grier, Lamar Lundy, and fellow Hall of Famer Merlin Olsen, which was lauded by Dick Butkus as "the most dominant line in football history". Additionally Jones is widely credited with coining the term "sack". His explanation of the term:

> Sacking the quarterback is just like you devastate a city or you cream a multitude of people. I mean, it's just like you put all the offensive players in one bag and I just take a baseball bat and beat on the bag.


### Comparing Players

To compare players across eras, we want to adjust for the number of games that players had. For players who play more games, frequently stats will note their progress at the previous number of games, e.g. using 16-game marks rather than full 17-game season totals. However, those extra games did in fact happen. It is just a relic of the schedule that the week 17 opponent occured in week 17 rather than in week 5. Thus, we can consider all 14 game subsets of a player's season to see the distribution of 14 game seasons that each player could have had given their performances in the 17 game season. By doing this, we are assuming that performances are independent week-to-week. One may argue that a coach has more information to game plan or would change their game plan based on previous performances, but for players in this rarified air, they are the first, second, and third parts of a coaches game plan. Additionally, I think it is reasonable to assume that these players are equally motivated in each game, so their play will be similar.

For our analysis, for each player, we will compute all 14 game subsets of a player's per-game sack performance. For each of these 14-game seasons, we can compute their sack total. Then, we can compute the proportion of 14-game seasons in which the player match or better Jones's best seasons with 22 sacks. If a player only reaches 22 sacks in a small subset of seasons, that suggests their total is more dependent on having more games. Below are each plot, along with a table of proportions.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/AlBaker.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/MylesGarrett.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/MichaelStrahan.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/TJWatt.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/JaredAllen.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
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


* Chart the course for the exploration
  * Acknowledge assumptions, limitations (check out LLM conversation for these)
  * Lay out intuition (why combinations?)
* Plots + proportions
* Interpretations
* Conclusions
