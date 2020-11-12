---
layout: default
title: Power Users
nav_order: 60
---


# Graph Filters

## Graph Keyword Filters 

## Distance Filters

# SQL Query Panel

## Database Schema
The following is the schema for the database which you query.  Every graph has a corresponding unique database.  

### `papers`
The table containing all of the papers in the graph

|              Column Name |    Type |                                                                                                                                                                        Description |
| -----------------------: | ------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                 paper_id | INTEGER |                                                                                                                                                        The unique id of the paper. |
|                      doi |    TEXT |                                                                                                                                                  The doi of the paper in question. |
|                  authors |    TEXT |                                                                                                                                      A json field of all the authors on the paper. |
|                    title |    TEXT |                                                                                                                                                            The title of the paper. |
|           published_year | INTEGER |                                                                                                                                                  The year the paper was published. |
|          published_month | INTEGER |                                                                                                                                                 The month the paper was published. |
|                  journal |    TEXT |                                                                                                                                      The journal in which the paper was published. |
|                   volume |    TEXT |                                                                                                                        The volume of the journal in which the paper was published. |
|                    issue |    TEXT |                                                                                                                         The issue of the journal in which the paper was published. |
|               book_title |    TEXT |                                                                                                                            The title of the book in which the paper was published. |
|               num_citing | INTEGER |                                                                                                                                      The number of papers which this papers cites. |
|             num_cited_by | INTEGER |                                                                                                                                        The number of papers which cite this paper. |
|                 distance | INTEGER |                                                                                                   The degrees away (as an undirected graph) this paper lies from the source paper. |
|                page_rank |    REAL |                                                                                                                                                        The PageRank of this paper. |
|              adamic_adar |    REAL |                    The Adamic/Adar score of the paper. Adamic/Adar is a link prediction algorithms which, when used in this context, can help to detect similarity between papers. |
|      resource_allocation |    REAL | Similar to Adamic/Adar, the Resource Allocation score of the paper is a link prediction algorithms which, when used in this context, can help to detect similarity between papers. |
|   conference_series_name |    TEXT |                                                                                                                       The name of the conference in which the paper was presented. |
| conference_instance_name |    TEXT |                                                             The instance of the conference in which the paper was presented. This is more specific than the conference_series_name |
|      conference_location |    TEXT |                                                                                                                      The location of the conference where the paper was presented. |
|          conference_year |    TEXT |                                                                                                                          The year of the conference where the paper was presented. |

### `authors`
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

### `title_terms`
A table a list of all of the stemmed title terms present in the full text index and their counts.

| Column Name | Type |                                          Description |
| ----------: | ---: | ---------------------------------------------------: |
|        term | TEXT | The porter-stemmed terms which appear in the titles. |
|   doc_count |  INT |    The number of papers in which these terms appear. |