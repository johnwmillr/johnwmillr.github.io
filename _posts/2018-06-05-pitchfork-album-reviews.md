---
title:  "Pitchfork album reviews"
date:   2018-06-05
layout: post
tag:
- python
- music
- lyrics
category: blog
author: john
name: john
image: assets/images/pitchfork_score_vs_lexdiv.png
description: Comparing Pitchfork album reviews and song lyrics
---

This post is very much a work in progress, but I wanted to share an interactive plot that I think is fun to play with. I've been scraping Pitchfork reviews using my fork of [@michalczaplinski's](https://github.com/michalczaplinski) excellent [Python wrapper](https://github.com/johnwmillr/pitchfork) for the [Pitchfork](https://pitchfork.com/) music website.

I've searched through my collection of [rap, rock, and country lyrics](http://www.johnwmillr.com/interactive-plots-in-jekyll/) and scraped reviews for albums that were reviewed on Pitchfork. The plot below compares the relationship between the lexical diversity of an album's lyrical content, and the review score the album received on Pitchfork.

Move your mouse over the points in the plot to see more detail about the albums they represent.

{% include mpld3_lexdiv_vs_score.html %}

There doesn't seem to be too strong of a correlation between lexical diversity and the Pitchfork score, but I plan to dig deeper into both sets of data to see what relationships there may still be.