---
layout: distill
title: Fire Risk Assessment Project
description: A semester project I worked on to learn about computer vision and convolutional neural network architectures
tags: distill formatting
giscus_comments: false
date: 2025-06-03
featured: false
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

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).

# toc:
# - name: Equations
# if a section has subsections, you can add them as follows:
# subsections:
#   - name: Example Child Subsection 1
#   - name: Example Child Subsection 2
# - name: Citations
# - name: Footnotes
# - name: Code Blocks
# - name: Interactive Plots
# - name: Mermaid
# - name: Diff2Html
# - name: Leaflet
# - name: Chartjs, Echarts and Vega-Lite
# - name: TikZ
# - name: Typograms
# - name: Layouts
# - name: Other Typography?
  
---

This post is a recap of a course project I worked on for a machine learning course. I was interested in learning how to implement some of the classic neural network architectures for image classification and apply them to something related to conservation. Forest fires are a natural disaster that can cause billions of dollars in damages, but they are also unique in that they humans are often the direct cause. Thus, we can potentially take action to help mitigate their destruction. For this project, I develop a tool that uses satellite data made available by {% cite gregor2015draw %} to identify areas with high risk of the breakout of a wildfire. The risk labels are determined by the Wildfire Hazard Potential index, a tool maintained by the USDA Forest Service. The scores are determined by wildfire simulation modeling. The associated images that make up the features of the model are collected from the National Agriculture Imagery Program, in which aircraft or satellites capture 60-cm ground sample distance images of agricultural and forest land. Each image is annotated with its longitude and latitude, making it easy to identify the risk label of the area captured in the image, as provided by the Wildfire Hazard Potential index.
