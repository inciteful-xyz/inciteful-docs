---
layout: default
title: Power Users
nav_order: 60
---
If you really want to get to know all the functionality of Inciteful, you've found the right place.

- [Beta Features](#beta-features)
- [Paper Discovery](#paper-discovery)
  - [Graph Filters](#graph-filters)
    - [Keyword Filters](#keyword-filters)
      - [Boolean Queries](#boolean-queries)
      - [Porter Stemming](#porter-stemming)
    - [Distance Filters](#distance-filters)
  - [SQL Query Panel](#sql-query-panel)
    - [Database Schema](#database-schema)
      - [`papers`](#papers)
      - [`authors`](#authors)
    - [`title_search('SEARCH_TERM')`](#title_searchsearch_term)
      - [`title_terms`](#title_terms)
- [Literature Connector](#literature-connector)
  - [Context (right-click) Options](#context-right-click-options)
  - [Graph Filters](#graph-filters-1)
    - [Keyword Filters](#keyword-filters-1)
    - [Extended Graphs](#extended-graphs)
- [BibTeX](#bibtex)
    - [Importing into Inciteful](#importing-into-inciteful)
    - [Mendeley: Exporting Citations to a BibTex file](#mendeley-exporting-citations-to-a-bibtex-file)
    - [Zotero: Exporting Citations to a BibTex file](#zotero-exporting-citations-to-a-bibtex-file)
  - [Exporting from Inciteful](#exporting-from-inciteful)

# Beta Features
Community feedback is invaluable.  That's why you can opt into features we are testing from our <a href="https://inciteful.xyz/beta">Beta Features</a> page.  Go boldly forth if you are the adventurous type. 
# Paper Discovery
## Graph Filters
On every graph dashboard there are a set of filters which allow you to filter the contents of the tables below.  This allows you to really dig into the graph and find the type of papers you are looking for.  The three types of filters are keywords, distance, and year.  

The year filter is pretty straight forward it filters on the year the paper was published. The other two need a bit more explaining.  

### Keyword Filters 
The keyword filters do just that, they filter on keywords present in the **title**.  Unfortunately we do not have access to abstracts at this point and so title filtering is the best we can do.  

We tried to make the search flexible.

#### Boolean Queries
The keyword filter does do Boolean queries.  So you can use the `AND`, `OR`, and `NOT` in your queries.  The following are all valid queries:

```
hello AND world
foo OR bar
(goodbye AND world) NOT cruel
```

You can join them together to your heart's content.

#### Porter Stemming
Also, the keywords you put in are subject to the [Porter Stemming Algorithm](http://people.scs.carleton.ca/~armyunis/projects/KAPI/porter.pdf) so that it will do partial matches on words.  For example, the following words would all match each other with the same stem of `connect`:

```
connect
connected
connecting
connection
connections
```

### Distance Filters
In order to really understand the distance filters you first need to understand [how the paper discovery tools works](paper-disovery-explained#building-local-graphs).  But I will do a quick rundown here. 

For graphs that are centered on a single `seed paper`: 

* the `seed paper` has a distance of `0`
* papers which either cite the `seed paper` or are cited by the `seed paper` have a distance of `1`
* papers which either cite or are cited by the papers with a distance of `1`, have a distance of `2` 

In visual form:

![](assets/images/depth-2-graph.png)

For papers which are centered around multiple `seed papers`:
* the "fake paper" we create has a distance of `0`
* the `seed papers` have a distance of `1`
* papers which either cite or are cited by the `seed papers` have a distance of `2` 

For a better understanding, head over to the [Paper Discovery Explained](paper-disovery-explained) page.
## SQL Query Panel

### Database Schema
The following is the schema for the database which you query.  Every graph has a corresponding unique database.  

#### `papers`
The table containing all of the papers in the graph

|    Column Name |    Type |                                                                                                                                                                                                                                       Description |
| -------------: | ------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|       paper_id | INTEGER |                                                                                                                                                                                                                       The unique id of the paper. |
|            doi |    TEXT |                                                                                                                                                                                                                 The doi of the paper in question. |
|        authors |    TEXT |                                                                                                                                                                                                     A json field of all the authors on the paper. |
|          title |    TEXT |                                                                                                                                                                                                                           The title of the paper. |
| published_year | INTEGER |                                                                                                                                                                                                                 The year the paper was published. |
|        journal |    TEXT |                                                                                                                                                                                                     The journal in which the paper was published. |
|         volume |    TEXT |                                                                                                                                                                                       The volume of the journal in which the paper was published. |
|    num_authors | INTEGER |                                                                                                                                                                                                               The number of authors on the paper. |
|     num_citing | INTEGER |                                                                                                                                                                                                     The number of papers which this papers cites. |
|   num_cited_by | INTEGER |                                                                                                                                                                                                       The number of papers which cite this paper. |
|       distance | INTEGER |                                                                                                                                                                 The distance away (as an undirected graph) this paper lies from the `seed paper`. |
|      page_rank |    REAL |                                                                                                                                                                                                                       The PageRank of this paper. |
|    adamic_adar |    REAL | The [Adamic/Adar](https://neo4j.com/docs/graph-data-science/current/alpha-algorithms/adamic-adar/) score of the paper. Adamic/Adar is a link prediction algorithm which, when used in this context, can help to detect similarity between papers. |
|         cocite |    REAL |                                         The co-citation score between two papers. We use the [Salton Index](https://cran.r-project.org/web/packages/linkprediction/vignettes/proxfun.html#salton-index-cosine-similarity) to calculate the score. |

#### `authors`
A denormalized table containing the metadata about each author for each paper.

| Column Name |    Type |                                                     Description |
| ----------: | ------: | --------------------------------------------------------------: |
|   author_id | INTEGER |                                    The unique id of the author. |
|    paper_id | INTEGER |                                     The unique id of the paper. |
|        name |    TEXT |                                         The name of the author. |
|    sequence | INTEGER |                        The sequence of the author in the paper. |
| affiliation |    TEXT | The affiliation of the author at the time the paper was written |

### `title_search('SEARCH_TERM')`
A table containing a full text index of the paper titles that can be searched by replacing {SEARCH_TERM} with the query of your choice. You can use Boolean operators like AND, OR, and NOT in addition to parenthesis to create matching logic. An example finding the best match:

```
SELECT * FROM title_search('refugee') ORDER BY bm25(title_search)
```

|        Column Name |    Type |                                                                                                                                             Description |
| -----------------: | ------: | ------------------------------------------------------------------------------------------------------------------------------------------------------: |
|           paper_id | INTEGER |                                                                                                                             The unique id of the paper. |
|              title |    TEXT |                                                                                                                            The text which was searched. |
| bm25(title_search) |    REAL | Returns a real value indicating how well the current row matches the full-text query. The better the match, the numerically smaller the value returned. |

#### `title_terms`
A table a list of all of the stemmed title terms present in the full text index and their counts.

| Column Name | Type |                                          Description |
| ----------: | ---: | ---------------------------------------------------: |
|        term | TEXT | The porter-stemmed terms which appear in the titles. |
|   doc_count |  INT |    The number of papers in which these terms appear. |

# Literature Connector

## Context (right-click) Options
The ability to right click on paper nodes in the graph is something that is not obvious but helps with exploring the graphs.  The right click menu quickly allows you to set a new "from" or "to" paper, add a paper to a new "paper discovery search", lock a the graph's paths to a particular paper, or jump directly to the "Paper Discovery" view of that single paper. 

![](assets/images/lc-right-click.png)
## Graph Filters
On every page there are a set of filters which allow you to filter the contents of the table and highlight matches in the graph.  This allows you to help you see the different clusters of papers.  The three types of filters are keywords, year, and Extended Graph.  

The year filter is pretty straight forward it filters on the year the paper was published. The other two need a bit more explaining.  

### Keyword Filters 
The keyword filters do just that, they filter on keywords present in the **title**.  Unfortunately we do not have access to abstracts at this point and so title filtering is the best we can do.  The keywords use [Porter Stemming](#porter-stemming) just like the paper discovery tool and unfortunately there is no boolean searching at this point. The keywords are all "AND".

### Extended Graphs
Often times when you are connecting two close papers the graph won't be that interesting.  The papers might be directly connected or are connected by just a few other papers.  As in this example: 

![](assets/images/close-papers.png)

So while it's interesting to see the three papers they have in common, you get more interesting results if you extend the paths by an extra level.  So in this case that means including all paths of three hops in addition to the paths of two hops.  The end result gives you a better overview of how these papers are interrelated:

![](assets/images/extra-layer.png)

Additionally things like the keyword cloud are better populated to give more context:

![](assets/images/extra-layer-kw.png)
# BibTeX
Inciteful supports both [BibTeX](faq#what-is-a-bibtex-file) importing as well as exporting. The import functionality is used to seed a graph and the export functionality is used to save papers that are of interest to you. 

### Importing into Inciteful
Instead of manually building up your network, you can use the import functionality to seed a network with papers in which you are already interested.  In order to do so, go to the home page and under the main search box there is an `Import BibTeX` link.  Click on that to use your BibTeX file as the basis for your search.  

**Note:** Inciteful will only recognize BibTeX entries with a [DOI](faq#what-is-a-doi) associated with them. So please be sure that your references have the appropriate DOIs.  If using Zotero, you can use the [Locate](https://www.zotero.org/support/locate) functionality to expedite this process. 

### Mendeley: Exporting Citations to a BibTex file
1. Select the references you wish to export to BibTex in Mendeley
2. Under the `File` menu item click `Export`
3. Then choose file type `BibTex (*.bib)`, save your BibTex file with a `.bib` extension

### Zotero: Exporting Citations to a BibTex file
1. Under the `My Library` menu on the left, right click on the folder you wish to export.
2. In the context menu click `Export Collection`
3. Then choose the `BibTex` format and click `OK`
4. Save your BibTex file with a `.bib` extension

## Exporting from Inciteful
At the bottom of every table which has a DOI in the data, there will be an export button (![](assets/images/bibtex-button.png)) which you can use to export the contents of the table in a BibTeX format. 
