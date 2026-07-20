---
layout: distill
title: Comparing Leads Across Sports
date: 2026-07-10 16:00:00
featured: false
description: How do leads compare across different sports?
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

This week, I was listening to the [Wharton Moneyball Podcast](https://open.spotify.com/show/7euXqPldw3dB4gX0HP2J5H?si=d51bd39ac5854adf) hosted by professors who discuss statistics in sports. Professor [Adi Wyner](https://statistics.wharton.upenn.edu/profile/ajw/) and one of his graduate student collaborators, [Jonathan Pipping](https://www.linkedin.com/in/jdpipping/), mentioned their [research from NESSIS 2025](https://www.youtube.com/watch?v=J0-GQnOtSkI) on win probabilities. While they focused on blown leads, it got me thinking about how different leads compare. In this post, I explore how different leads compare across soccer, basketball, and American football. Conditional on time elapsed in the game and score differential, I estimate the probability that the home team will win the game by simply taking the proportion of home teams that have won the game in the data. Previous research from Wyner and Ryan Brill demonstrate that the complexity in estimating win probability is not adequately appreciated, and factors such as selection bias lead to biased estimates that don't properly communicate the uncertainty<d-cite key="brillHumility"></d-cite><d-cite key="brillHumilitySim"></d-cite>. With this in mind, my model certainly does not capture all of the intricacies of estimating win probability. However, conditioning on team quality and game state factors would make comparisons across sports more difficult, as those variables would inherently be intertwined with the specific rules of the game, whereas time elapsed is common to all sports studied, and works commonly in each of them. 

Part of the inspiration for this post is the World Cup. While I am an informed consumer of basketball and American football, I know almost nothing about soccer. Thus, when I'm watching a game, it's hard for me to discern when a team no longer has a reasonable chance to win the match. With this post, I hope to understand, roughly, what a 2 score lead in the 65th minute means in terms of basketball scoring.

### Soccer
The first sport I want to look at is soccer. The data comes from [StatsBomb](https://github.com/statsbomb/open-data/tree/master), who provide a wonderful dataset of event-level data for thousands of games. For our purposes, I focused on men's soccer, and only international competition or matches from top European leagues. These were the Premier League, La Liga, Bundesliga, Serie A, Ligue 1, Champions League, or UEFA Europa League. In total, there were 2524 matches from a variety of years.

- INCLUDE TIES IN COMPUTATION OF WIN PROBABILITIES

<div class="l-page">
  <iframe src="{{ '/assets/plotly/soccer2.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>


### Basketball
- Which leagues
- I think it'll be `hoopsR`
- Update plot to have data from more years than just last season!
- I like including games that went to overtime in the win probability averaging, but plotting them really muddies the plot, so maybe delete that portion of the plot?

<div class="l-page">
  <iframe src="{{ '/assets/plotly/basketball.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

### Football
- I think it'll be `nflFastR`
- 2018 through 2025 regular season games (after a rule change to over time)
- I'm going to remove leads/deficits of 17 points or more, but include a stat or two in writing
  - 3.8% of teams down 17+ at half time have come back to win the game in the regular season
 
<div class="l-page">
  <iframe src="{{ '/assets/plotly/football.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

### Putting it together

I think a table where you can sort by empirical win rates and from there see what sorts of times and leads are comparable. There will be a ton of times so... 
<div id="wp-controls">
  <label>
    Sport
    <select id="wp-sport">
      <option value="football">Football</option>
      <option value="basketball">Basketball</option>
      <option value="soccer">Soccer</option>
    </select>
  </label>

  <label>
    Time elapsed
    <select id="wp-time"></select>
  </label>

  <label>
    Score differential
    <select id="wp-diff"></select>
  </label>
</div>

<script>
  window.addEventListener('load', function () {
    const sportSelect = document.getElementById("wp-sport");
    const timeSelect = document.getElementById("wp-time");
    const diffSelect = document.getElementById("wp-diff");

    const maxTimeBySport = {
      football: 60,
      basketball: 48,
      soccer: 90,
    };

    const maxDiffBySport = {
      football: 16,
      basketball: 30,
      soccer: 3,
    };

    function populateTimeOptions() {
      const sport = sportSelect.value;
      const maxTime = maxTimeBySport[sport];

      timeSelect.innerHTML = "";

      for (let t = 0; t <= maxTime; t += 3) {
        const opt = document.createElement("option");
        opt.value = t;
        opt.textContent = `${t} min`;
        timeSelect.appendChild(opt);
      }
    }

    function populateDiffOptions() {
      const sport = sportSelect.value;
      const maxDiff = maxDiffBySport[sport];

      diffSelect.innerHTML = "";

      for (let d = -maxDiff; d <= maxDiff; d += 1) {
        const opt = document.createElement("option");
        opt.value = d;
        opt.textContent = d > 0 ? `+${d}` : `${d}`;
        diffSelect.appendChild(opt);
      }

      // default to 0 differential (tied game) if it's present
      diffSelect.value = "0";
    }

    function handleSportChange() {
      populateTimeOptions();
      populateDiffOptions();
    }

    handleSportChange();
    sportSelect.addEventListener("change", handleSportChange);
  });
</script>
