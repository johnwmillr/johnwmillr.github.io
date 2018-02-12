---
title:  "Trucks and beer"
date:   2018-02-07
layout: post
tag:
- python
- music
- lyrics
category: blog
author: john
description: Analyzing country music lyrics
---

Inspired by a post on [Big-ish Data](https://bigishdata.com/2016/10/25/talkin-bout-trucks-beer-and-love-in-country-songs-analyzing-genius-lyrics/), I've started working on a textual analysis of popular country music.

More specifically, I scraped [Billboard.com](https://www.billboard.com/charts/year-end/2017/top-country-artists) for a list of the top 50 country artists from 2017 and used my Genius API [python wrapper](https://github.com/johnwmillr/GeniusLyrics) to download the lyrics to each song by every artist on the list. After my script ran for about five hours, I was left with 5,089 songs across 50 artists stored in a 7 MB JSON file. I then realized the Billboard Top 50 list disproportionately included men, so I ran the script again overnight on a list of the best female country artists from [Ranker.com](https://www.ranker.com/crowdranked-list/top-female-country-singers). After combining the two lists and requiring a minimum of 20 songs per artist, I was left with 7,712 songs across 60 artists.

You can find my code for this project [on Github](https://www.github.com/johnwmillr/song-lyrics-analysis).

Some pertinent questions:
  - Which artist mentions trucks in their songs most often?
  - Does an artist's affinity for trucks predict any other features? Their gender for example? Or their thirst for beer?
  - How does the mention of trucks vary with time? Each song item contains its publishing date.
  - Of the fifty artists, whose language is most unique? Whose is most generic?

---
# Visualizations

### Word usage relationships
I'm interested in whether an artist's tendency to use certain terms correlate together. For example, if an artist is more likely to mention beer in their songs, are they more likely to also mention trucks? It turns out that yes, they are.


Each point on the word-frequency plots represents a single artist. The values for each point were calculated as a simple percentage of times the given artist mentions a particular term. For example, Cole Swindell had 46 total songs and mentioned beer in 24 of them, arriving at a mention percentage of 52%.

![beer_and_trucks]({{site.url}}/assets/images/FreqPlot_beer_and_truck.png)

I've also added the artist's gender to the plot. Further analysis is needed, but there does appear to be an interaction between gender and one's likelihood to sing about trucks and beer. I haven't found a good way to display this yet, 50% of the female artists are actually stacked on top of each other at the origin, meaning they didn't mention beer or trucks in any of their songs.


I also took a look at the relationship between an artist's use of the words "girl" and "love". There appears to be an interaction with gender here too. A male country singer is less likely to mention love the more often he uses the word "girl" in his songs. Interesting.

![girl_and_love]({{site.url}}/assets/images/FreqPlot_girl_and_love.png)

### Vocabulary over time
I also wanted to look at how vocabulary changes over time for all country artists. We know from the plot above that male country artists are less likely to sing about love and more likely to sing about girls. That plot combined songs from all years -- I wonder how the effect changes if we take time into account?

I was curious to see how certain terms become more and less popular over time. The plot below displays the percentage of songs mentioning a given term for each year. Years with less than ten songs in my database were excluded. It looks like it's becoming less common for country artists to mention love in their songs. While still about 50% of country songs from 2017 mention love, roughly 75% of country songs in the 1960's mention love. As love gets mentioned less frequently, it's becoming more common for country songs to include the word "girl".

![vocab_over_time]({{site.url}}/assets/images/TimePlot_girl_boy_love.png)



