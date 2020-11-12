---
layout: default
title: How Does Inciteful Work?
nav_order: 50
---

In order to understand how Inciteful works, you should have a base line level of knowledge about graphs.  If you don't, read [Graphs Explained](graphs-explained.md) first and then come back here. 

- [Academic Papers as Graphs](#academic-papers-as-graphs)
  - [As a Directed Acyclic Graph](#as-a-directed-acyclic-graph)
- [Local Graphs](#local-graphs)
  - [Starting with a Paper](#starting-with-a-paper)
  - [Making Your Own Graph](#making-your-own-graph)
- [Algorithms](#algorithms)
  - [What is PageRank?](#what-is-pagerank)
  - [Link Prediction Algorithms](#link-prediction-algorithms)
- [The Underlying Data](#the-underlying-data)


# Academic Papers as Graphs
One way to think about the body of academic literature is as one big graph with the papers serving as the nodes and citations serving as the edges connecting the vertices.  When conceptualized as such, you are able to apply an entire area of mathematics, called graph theory, to academic literature.  As it turns out, there are certain classes of problems in graph theory, the solutions to which, are helpful in analyzing the academic graph.  

But before we dive into the [algorithms](#algorithms) we use, let's think a talk a bit more about specifically what type of graph the academic literature forms.  

## As a Directed Acyclic Graph
If you think about how academic literature evolves the underlying structure of the graph becomes apparent and it has implications for what types of algorithms we can use as well as the real world meaning of the results.  The two most important factors are:

* Citations are a one way relation.  `Paper A` citing `Paper B` does not mean that `Paper B` also cites `Paper A`.  As a result, the graph is what we call "[directed](graphs-explained#directed-vs-undirected)".
* Academic literature is inherently subject to time, i.e. papers can only cite what has already been published.  As a result, there is no way for loops to form in the graph. 

These two points, happen to satisfy the requirements for calling the academic graph a **directed acyclic graph** or (DAG) <sub>[[wikipedia]](https://en.wikipedia.org/wiki/Directed_acyclic_graph)</sub>.  Understanding this, helps us to understand how to interpret the results and implications of our later analysis. 

# Local Graphs
The entire graph of academic literature is too big to efficiently analyze as one giant graph. Additionally a lot of information in the graph is totally irrelevant to the question you want answered.  As a result, we try to make a localized graph specific to your query.  The normal starting point is with a single paper but the goal is to create a custom graph centered around the topic of your choice.   

## Starting with a Paper
When you start with a paper (we call it the source paper), Inciteful builds a network around the source paper by finding all of the papers which that papers cites and which cite that paper.  The we do it again with all of those papers we found in the first search.  The resulting graph looks similar to this: 

![](assets/images/depth-2-graph.png)

Where the node labeled `0` represents the source paper, the nodes labeled `1` represent the results of the first search, and the nodes labeled `2` represent the results of the second search.  In this process we also capture all of the citations between the nodes in level two as well.  From here we run a few different algorithms against this graph to find the most interesting papers. 

## Making Your Own Graph
The core idea of Inciteful is to enable you to make your own personalized graph.  So as you find papers that are interesting, you can start to add them to the graph to make it more centered around your topic.  When you have more than one paper building the graph, we consider these `seed papers`

Behind the scenes this is accomplished by "faking" the graph.  Essentially when you add multiple papers to a graph Inciteful creates a fake node that acts as if it cites the papers you added to the graph.  

What that means for the graph we just saw is that node `0` isn't an actual paper and there would be no citations coming into that node, because no one cites a fake paper... and so we flipped that citations and made it red.  The `seed papers` are the nodes labeled `1` and the nodes labeled `2` are all of the papers which are cited by or cite the `seed papers`.

![](assets/images/lr-graph.png)

Also, all of the algorithms we run that predict things like similarity are relative to this "fake" node `0`.   It's helpful to understand this structure as you are trying to filter the graphs based on depth or interpret the results of different algorithms. 

# Algorithms

## What is PageRank? 

## Link Prediction Algorithms

# The Underlying Data

- Microsoft Academic Graph 

- Semantic Scholar

- Unpaywall

- Crossrefs

- Open Citations