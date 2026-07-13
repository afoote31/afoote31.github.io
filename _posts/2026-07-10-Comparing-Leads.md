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

This week, I was listening to the [Wharton Moneyball Podcast](https://open.spotify.com/show/7euXqPldw3dB4gX0HP2J5H?si=d51bd39ac5854adf), a podcast hosted by statistics professors who discuss statistics in sports. Professor [Adi Wyner](https://statistics.wharton.upenn.edu/profile/ajw/) and one of his graduate student collaborators, [Jonathan Pipping](https://www.linkedin.com/in/jdpipping/), mentioned their [research from NESSIS 2025](https://www.youtube.com/watch?v=J0-GQnOtSkI) on win probabilities. While they focused on blown leads, it got me thinking about how different leads might compare in different sports. I want to explore that in this blog post.

#### Basic Setup:
- Data of game scores at minute-level
- Who wins
- Win probabilities, conditional on lead and time remaining for different sports
- Line charts are interesting, might want to explore resampling to get estimates of variability
- Acknowledge that estimating win probabilities is very difficult so this is only a rough estimate (cite Wyner paper)
- Goal is to compare roughly, and introducing tons of conditioning or strata makes those comparisons less meaningful


### Soccer
- Data from lots of leagues
- Reference StatsBomb
- INCLUDE TIES IN COMPUTATION OF WIN PROBABILITIES

<div class="l-page">
  <iframe src="{{ '/assets/plotly/soccer.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
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

I think a table where you can sort by empirical win rates and from there see what sorts of times and leads are comparable. There will be a ton of times so 


<div id="blog-post-table"></div>

<link href="https://unpkg.com/tabulator-tables@5.6.1/dist/css/tabulator.min.css" rel="stylesheet">
<script src="https://unpkg.com/tabulator-tables@5.6.1/dist/js/tabulator.min.js"></script>

<style>
  #my-table {
    margin: 2rem 0;
    font-size: 0.9rem;
  }
  /* optional: match al-folio's theme a bit more closely */
  .tabulator {
    border: 1px solid var(--global-divider-color, #ddd);
    border-radius: 6px;
  }
</style>

<script>
  // Replace this with your real data, or load from a JSON/CSV file in assets/
  const tableData = [
    {id: 1, name: "Alpha",   category: "Model",   score: 92, year: 2023},
    {id: 2, name: "Beta",    category: "Dataset",  score: 78, year: 2022},
    {id: 3, name: "Gamma",   category: "Model",   score: 85, year: 2024},
    {id: 4, name: "Delta",   category: "Method",  score: 67, year: 2021},
    {id: 5, name: "Epsilon", category: "Dataset",  score: 90, year: 2023},
    {id: 6, name: "Zeta",    category: "Method",  score: 73, year: 2022},
    {id: 7, name: "Eta",     category: "Model",   score: 88, year: 2024},
    {id: 8, name: "Theta",   category: "Dataset",  score: 81, year: 2023},
    // ... add as many rows as you need
  ];

  const table = new Tabulator("#my-table", {
    data: tableData,
    layout: "fitColumns",
    pagination: true,
    paginationSize: 5,               // rows per page
    paginationSizeSelector: [5, 10, 20, 50, true], // "true" = "All" option
    paginationCounter: "rows",        // shows "Showing X-Y of Z rows"
    columns: [
      {title: "ID", field: "id", width: 60, sorter: "number"},
      {
        title: "Name",
        field: "name",
        headerFilter: "input",        // free-text search on this column
        sorter: "string"
      },
      {
        title: "Category",
        field: "category",
        headerFilter: "list",         // dropdown-style filter
        headerFilterParams: {
          valuesLookup: true,         // auto-populates dropdown from data
          clearable: true
        },
        sorter: "string"
      },
      {
        title: "Score",
        field: "score",
        headerFilter: "number",
        headerFilterPlaceholder: "min score",
        headerFilterFunc: ">=",       // filter shows rows >= entered value
        sorter: "number"
      },
      {
        title: "Year",
        field: "year",
        headerFilter: "list",
        headerFilterParams: {valuesLookup: true, clearable: true},
        sorter: "number"
      },
    ],
  });
</script>
