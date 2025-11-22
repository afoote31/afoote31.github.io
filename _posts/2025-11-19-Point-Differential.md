---
layout: distill
title: The Impact of Tanking on NBA Team Ratings
description: Some work I've done on applying survival analysis tools to help fill out brackets.
tags:
giscus_comments: true
date: 2025-11-19
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
hidden: true

authors:
  - name: Aaron Foote

bibliography: 2018-12-22-distill.bib

---
**FIND THE PODCAST WHERE THEY TALKED ABOUT THIS! I think the thought for point differential might also extend to things like wins.**

I think I want to frame this as an exploration of the point differential metric in the NBA. First, explain how some teams are doing really well this season, and some very poorly. Importantly, more teams are doing very poorly than usual. **I need to do more literature review to see what other people say about point differential**. In the post I want to explore vanilla point differential as well as some modifications to it. My hope is that we can improve our understanding of point differential as a statistic, it's assumptions and limitations, and through this process settle on a statistic akin to point differential that better rates team quality but is still interpretable.

## Background

- What other people say about point differential
- Other systems that have been proposed (simple as well as model-based)
  - Adjusted Scoring Margin
  - SRS Simple Rating System
  - Net Rating (possession-adjusted scoring and points allowed)
  - Elo systems
- Commonly cited shortcomings
  - Blowouts and ignoring game context
    - Blowouts --> Second units and different strategies that are not representative of team quality
    - Close games --> Warped version of basketball with lots of fouling
  - Parity
  - Pace of play
  - Doesn't account for recent injuries
    - It's sort of a weighting of all performances evenly, so a recent injury will not be reflective of team quality
  - In sports other than the NBA, you have much bigger variance in point differentials since scoring is a much rarer event in those sports
  - We're assuming that teams have roughly the same strength of schedule across an 82 game season, and things like injuries play a much greater role in point differentials than strength of schedule

## Blowouts
- Taking only the first three quarters
- Removing play when margins go above a certain threshold

## Parity

Point differential in the NBA is a very commonly used stat to measure the strength of a team. People like it because it feels intuitive. I'm concerned that it's not so intuitive.This year, in the NBA, there are more teams than usual that STINK. The three to five worst teams in the NBA this year are worse than the three to five worst teams in the NBA in previous years. I think that this results in the rest of the teams having higher point differentials than would other teams at their point differential ranking historically. If this is the case, then the best teams having really good point differentials might not be so comparable to years past. 

1. See where teams this year place in point differential relative to teams that have the same rank as them in point differential in previous years.
2. How does point differential minus average point differential look?
3. What happens when you only consider the first three quarters, for both approaches?

To begin to analyze this, I want to get NBA game scores for the past years and compute the point differential for each team. Once I have that, I can rank each team by point differential. Then, for each rank, I want to see how point differentials for this season compare to typical teams ranked there. I'm guessing that for the top teams, you'll see them above standard, while for the worst teams, you'll see them below. I'm not sure what I'll see for the middle 70% of teams, but I'm guessing I would see a slight bias to being above the typical point differential. **I could visualize this with a histogram for each rank, or I could get the percentile rank of the 2025 teams at each rank and put it in a table**. I could also try looking at just the bottom four and top four teams. I could then plot the point differentials for the top four on one plot and bottom four on another, with the rank shown by color. That might lose some nuance but gain sample size. 

If we find that point differentials are kinda the same, then I need to think about whether I'm measuring this the right way or decide that there is nothing here and maybe write it up in my failed research ideas blog post. Suppose something is found though. I think that the next thing to do would be to try and correct for it in some way. I would like the solution to be intuitive and easy for a fan to understand. The first thing to do would be to 
