---
layout: default
title: How Does Inciteful Work?
nav_order: 50
---

In order to understand how Inciteful works, you should have a base line level of knowledge about graphs.  If you don't, read [Graphs Explained](graphs-explained.md) first and then come back here. 

- [Academic Papers as Graphs](#academic-papers-as-graphs)
  - [Directed Acyclic Graphs (DAGs)](#directed-acyclic-graphs-dags)
- [Local Graphs](#local-graphs)
  - [Starting with a Paper](#starting-with-a-paper)
  - [Making Your Own Graph](#making-your-own-graph)
- [Algorithms](#algorithms)
  - [What is PageRank?](#what-is-pagerank)
  - [Link Prediction Algorithms](#link-prediction-algorithms)
- [The Underlying Data](#the-underlying-data)
  - [Microsoft Academic Graph](#microsoft-academic-graph)
  - [Semantic Scholar](#semantic-scholar)
  - [Unpaywall](#unpaywall)
  - [Crossrefs](#crossrefs)
  - [Open Citations](#open-citations)


# Academic Papers as Graphs
One way to think about the body of academic literature is as one big graph with the papers serving as the nodes and citations serving as the edges connecting the vertices.  When conceptualized as such, you are able to apply an entire area of mathematics, called graph theory, to academic literature.  As it turns out, there are certain classes of problems in graph theory, the solutions to which, are helpful in analyzing the academic graph.  

But before we dive into the [algorithms](#algorithms) we use, let's think a talk a bit more about specifically what type of graph the academic literature forms.  

## Directed Acyclic Graphs (DAGs)
If you think about how academic literature evolves the underlying structure of the graph becomes apparent and it has implications for what types of algorithms we can use as well as the real world meaning of the results.  The two most important factors are:

* Citations are a one way relation.  `Paper A` citing `Paper B` does not mean that `Paper B` also cites `Paper A`.  As a result, the graph is what we call "[directed](graphs-explained#directed-vs-undirected)".
* Academic literature is inherently subject to time, i.e. papers can only cite what has already been published.  As a result, there is no way for loops to form in the graph. 

These two points, happen to satisfy the requirements for calling the academic graph a **directed acyclic graph** or (DAG).

Understanding this, helps us to understand how to interpret the results and implications of our later analysis. 

# Local Graphs
The 

## Starting with a Paper

## Making Your Own Graph

# Algorithms

## What is PageRank? 

## Link Prediction Algorithms

# The Underlying Data

## Microsoft Academic Graph 

## Semantic Scholar

## Unpaywall

## Crossrefs

## Open Citations