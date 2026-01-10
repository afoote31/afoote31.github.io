---
layout: distill
title: Where Does Myles Garrett's Season Stack Against All Time Great Sack Seasons?
description: With Myles Garrett breaking the official sack record, I wanted to explore how it compares to other all time great pass rushers. 
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

In the 2025 NFL regular season, Myles Garrett chasing the all time single season sack record was one of the main storylines. After a productive start to the season, Garrett cooled off between weeks three and seven, before exploding for 13 sacks in four weeks. After that, the race was on! This performance comes on the heels of him becoming (temporarily) the highest paid non-quarterback player in NFL history in the offseason, inking a contract worth \$160 million with \$123 in guaranteed money. 

However, it took him until the final game of the season to earn the record, meaning it took him 17 games. This has led some critics to discredit the record as the byproduct of more opportunities. Some even take issue with the way that Joe Burrow fell to the ground when pressured by Garrett, although it certainly doesn't have the same optics as the Strahan sack on Favre in 2001.

Putting this monumental achievement in the context of other all time seasons is difficult given the different play styles in different eras. For instance, offenses have become considerably more pass-heavy over time, giving defenders more opportunities to sack the quarterback (see plot below). On the other hand, ever since Bill Walsh turned football on its head with the introduction of the west coast offense first in Cincinnati under Paul Brown (1968-1975) before architecting a dynasty with the 49ers using the scheme, short passing has become more and more popular, decreasing the quality of the opportunities that pass rushers receive. In recent years, rich data sources such as that provided by the [Kaggle NFL Big Data Bowl](https://www.kaggle.com/competitions/nfl-big-data-bowl-2026-analytics) have allowed new stats to be developed that are better able to account for these nuances. However, the differences are still difficult to account for historically. On top of all of this, sacks were not counted as an official statistic until 1982, leaving only unofficial counts for many Hall of Famers. In this post, I will be considering unofficial sack totals.


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/passingYards.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Average pass attempts per game in the NFL each season, with top sack seasons colored red.
</div>




For this post, we will be taking the sack totals at face value, admittedly a limitation. I will be considering the players that equaled or bettered Deacon Jones's 1967 season with 21.5 sacks, yielding eight players along with Jones. The players and their seasons are:

| Player            | Sack Total    | Season        | Games Played  |
| :-----------      | :------------:|:------------: |:-------------:|
| Al Baker          | 23            | 1978          | 16            |
| Myles Garrett     | 23            | 2025          | 17            |
| Michael Strahan   | 22.5          | 2001          | 16            |
| TJ Watt           | 22.5          | 2021          | 15            |
| Jared Allen       | 22            | 2011          | 16            |
| Mark Gastineau    | 22            | 1984          | 16            |
| Justin Houston    | 22            | 2014          | 16            |
| Deacon Jones      | 22            | 1964          | 14            |
| Deacon Jones      | 22            | 1968          | 14            |
| Coy Bacon         | 21.5          | 1976          | 16            |
| Deacon Jones      | 21.5          | 1967          | 14            |

### The Greatness of Deacon Jones

Although the totals are unofficial, Deacon Jones's totals are truly incredible given that he only had 14 games. His trademark pass rush move, the head slap, would not be legal today, but I have no doubt that he would have been one of the all time greats in any era. Over his remarkably consistent 14 seasons, he played primarily for the Rams, forming the "Fearsome Foursome" alongside Rosey Grier, Lamar Lundy, and fellow Hall of Famer Merlin Olsen, which was lauded by Dick Butkus as "the most dominant line in football history". Additionally Jones is widely credited with coining the term "sack". His explanation of the term:

> Sacking the quarterback is just like you devastate a city or you cream a multitude of people. I mean, it's just like you put all the offensive players in one bag and I just take a baseball bat and beat on the bag.

With that established, I want to consider just how impressive the seasons that match or eclipse Jones's impressive numbers are. 

### Comparing Players
* Chart the course for the exploration
  * Acknowledge assumptions, limitations (check out LLM conversation for these)
  * Lay out intuition (why combinations?)
* Plots + proportions
* Interpretations
* Conclusions
