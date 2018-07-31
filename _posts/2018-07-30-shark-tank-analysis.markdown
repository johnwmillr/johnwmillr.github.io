---
title: "Analyzing data from deals on Shark Tank"
date: 2018-07-16
layout: post
tag:
- python
- data science
- API
category: blog
author: john
image: assets/images/sharktank_gender.png
description: Playing with Shark Tank data
---

## Introduction
<!-- Intro / interest in Shark Tank / description of show -->
My brother and I are big fans of [*Shark Tank*](https://abc.go.com/shows/shark-tank). For the uninitiated, *Shark Tank* is a fun show on ABC where hopeful entrepreneurs pitch their business ideas to a panel of "Sharks" (wealthy business magnates) in hopes of receiving making a deal that will allow them to take their business to the next level.

<!-- Pose the problem / question -->
After my brother and I watched a few episodes together on vacation recently, I started to wonder whether it'd be possible to identify any patterns or biases in the way Sharks make deals on the show. For instance, are male Sharks more likely to make deals with men than women? Or, for that matter, are male entrepreneurs more likely to make it on the show in the first place?

## Collecting the data
<!-- Describe Tecco's analysis -->
As I suspected, I wasn't the first to ask these sorts of questions. In a detailed post on Quora, Halle Tecco described her [analysis](https://www.quora.com/What-have-you-learned-from-watching-the-television-program-Shark-Tank/answer/Halle-Tecco) of the show. Amongst other insights, Halle found that across the first six seasons of the show, the two female Sharks (Barbara Corcoran and Lori Greiner) made a larger percentage of their deals with women than the male Sharks.

Halle made the data she collected available [online](https://docs.google.com/spreadsheets/d/1Lr0gi_QJB_JU0lBMjJ7WiBRxA0loml1FlM-KlmKsaEY/edit#gid=1213351262). I also [scraped](https://github.com/johnwmillr/SharkTank/blob/master/scrapeSharkTankData.ipynb) the Sharks' attendance records from a [Wikipedia page](https://en.wikipedia.org/wiki/List_of_Shark_Tank_episodes) so that I could know which pitches each Shark was actually present for.

## Posing a question
<!-- Okay, cut to the chase. What's this post about? -->
It's worth noting that the percentage of men and women appearing on the show is not 50/50---the ratio of all-male teams to all-female teams is closer to 70/30. I was curious to see how the Sharks' funding probabilities might change if I accounted for this imbalance.

The question I kept asking myself was, "what percentage of offers from either gender did each Shark make a deal with?". In other words, if a Shark heard pitches from 100 men and 100 women, how many of either gender did they then make a deal with? Posing the question in this way allows us to account for an unequal number of male and female entrepreneurs appearing on the show.

By combining the deal data from Halle's analysis with the attendance records I scraped from Wikipedia, I was able to answer the question I posed above.

[![Funding on *SharkTank* by gender](/assets/images/shark_tank_funding.png){: .center-image }](https://www.reddit.com/r/dataisbeautiful/comments/8wr8ko/funding_probabilities_on_shark_tank_grouped_by/)

Each bar represents the percent of entrepreneurs of a given gender that the Shark made a deal with. For example, Mark Cuban made deals with 20.2% of the women and 17.1% of the men whose pitches he saw on the show.

## Discussion
It's important to consider what question this graph is actually answering. Can we conclude from this graph that Corcoran and Herjavec somehow discriminate against male and female entrepreneurs respectively? Of course not. It's impossible (irresponsible even!) to look at a single variable (gender, in this case) and attempt to make sweeping generalizations about the show. And this graph does not attempt to make a broad conclusion! It simply presents the data (accurately) and allows the viewer to draw their own conclusions.

In my mind, the simple conclusion to draw from this graph is that there are gender imbalances in the deals certain Sharks make. The obvious next step is to ask questions about what might be contributing to this imbalance. The *wrong* step is to immediately conclude that the Sharks are sexist and avoiding deals with entrepreneurs of a gender different from their own.

As pointed out in [numerous comments](https://www.reddit.com/r/dataisbeautiful/comments/8wr8ko/funding_probabilities_on_shark_tank_grouped_by/e1y6wly/) on my Reddit post, there are many factors at play here. For one, Barbara Corcoran invests primarily in the food and beverage companies and Robert Herjavec in tech, two industries with quite different demographics. Additionally, the data I collected did not contain information on which Sharks made offers that were not accepted, meaning my graph does not account for the potential bias on behalf of the entrepreneurs, in terms of who they choose to accept a deal from.
