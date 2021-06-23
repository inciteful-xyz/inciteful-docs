---
layout: default
title: Getting Started
nav_order: 1
---

# What is Inciteful?
Inciteful is a new take on the process of searching through academic literature and, as such, can be a bit confusing at first.  The hope is that after a few minutes with these pages you'll quickly get the hang of it. 

## Our Tools
Right now Inciteful consists of two different tools with more under active development.  

The first tool was our Paper Discovery tool.  It builds a network of papers from citations, uses network analysis algorithms to analyze the network, and gives you the information you need to quickly get up to speed on that topic. You can find the most similar papers, important papers as well as prolific authors and institutions.

The second tool was our Literature Connector. Intended for interdisciplinary scholars trying to bridge two domains, it allows you to enter two papers and it will give you an interactive visualization showing you how they are connected by the literature. From there you can send the papers you find into our Paper Discovery tool to find other relevant literature which happened to not be the "shortest path" between the two papers.
## Getting Started
The site was built from the ground up to be flexible.  That means whether you are just skimming or are a power user, you should be able to accomplish what you need. 

* Go straight to the [Quick Start](quick-start) section if you are the type who just wants to dive right in and figure it out as you go.

* The [Use Cases](use-cases) section goes into different ways of using Inciteful.

* The [Paper Discovery Explained](paper-disovery-explained) page is for those who want to get into the details of the Paper Discovery Tool

* The [Power Users](power-users) section goes in depth on how to get exactly the info you want out of the graph using the SQL query interface.  

## Why Inciteful?
The vast majority of academic search engines focus on "importance" (as measured by number of citations) and keyword matching to retrieve their results. They typically show you stats about who the papers cite and who cites those papers. But there is value and information in the underlying structure that citations provide and it is almost always ignored. Inciteful flips that on it's head by making citations the center of it's search process by:

* Building a citation network centered around the paper(s) of your choice
* Analyzing that network to surface the most interesting data

Each network, and the data within, is unique to your search based on the papers you gave it so you can be sure to get the most relevant results possible. With Inciteful's unique approach you are presented not only with the most "important" papers in the graph, but also the most similar. This similarity measurement is from a class of algorithms called "link prediction" algorithms. 

Link prediction algorithms are used most commonly in social networks to suggest people with whom you should be friends. The same concept is applied here but for citations i.e. who we think you might want to cite. This approach tends to surface more recent literature and helps you zero in on the state of the art more quickly than if you were just looking for the top cited papers.  If you are interested in learning more, head over to our [Paper Discovery Explained](paper-disovery-explained) and [Graphs Explained](graphs-explained) sections. 

Otherwise jump into the [Quick Start](quick-start) section to dive right in. 