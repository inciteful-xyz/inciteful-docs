---
layout: default
title: Quick Start
nav_order: 20
---

# Quick Start
There are a variety of ways to use Inciteful, which you can view on on the [use cases](use-cases) page but here we will just go through a simple search process. 

## 1) Start with a Paper
The easiest way to get started is by having a paper that covers a topic in which you are interested.  You can either use the search box to type in the title or enter the [DOI](faq#what-is-a-doi) of the paper if you can't find it through the search.  For this example we will use the following as the source paper but you can use whatever you'd like:

[“Planning Dissonance” and the Bases for Stably Diverse Neighborhoods: The Case of South Seattle](https://inciteful.xyz/p/10.1111/cico.12224){:target="_blank"}

## 2) Explore the Results
At the top of the page we have information about the source paper such as the title, authors, journal it was published in, etc.  In addition to those we have basic stats about how many papers are citing this paper, how many papers the source paper cites, an open access link if applicable, as well as some information about the graph.  

![Graph Stats](assets/images/qs-graph-stats.png)

In this instance, it is a depth 2 graph, with 6,387 papers and 51,973 citations.  To better understand what this means in the context of Inciteful head over to [Graphs Explained](graphs-explained). 

### Important Papers
We'll skip past the `Filters` section and head down to the tables.  The first table covers the "Most Important" papers, as measured by the [PageRank](graphs-explained#what-is-page-rank) algorithm.  PageRank goes beyond simple citation counts and it values papers which are cited by other important papers, so you don't need to have a lot of citations to be important, just be cited by imporant papers. 

![Important Papers](assets/images/qs-important.png)

Given the nature of academic literature and how it takes time to build up citations, these papers tend to be the older papers in the graph.  They typically represent the seminal papers in the field.  

### Similar Papers
This section uses a [link prediction algorithm](graphs-explained#link-prediction-algorithms) to show you the most similar papers based on who these papers cite.  If the source paper cites many of the same papers that another paper does, then they are considered similar. 

![Similar Papers](assets/images/qs-similar.png)

The effect of similar papers is the inverse of important papers.  Since papers which are published after the source paper have a better chance of citing the same papers, these papers tend to be more recent papers in the field.

### Other Data
Under the similar papers section we have the Other Data section.  This section is used to highlight other interesting information about the graph.  Such as most important authors, institutions, and journals.  It helps to get an idea of where the work is being done and published. 

### Filters
Coming back to 
## 3) Add Relevant Papers

## 4) Create the Next Graph

## 5) Repeat Steps 3 and 4

## 6) Download the Results