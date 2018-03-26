---
title:  "Interactive plots in Jekyll"
date:   2018-03-25
layout: post
tag:
- python
- music
- lyrics
category: blog
author: john
name: john
image: assets/images/Plot_like_love.png
description: Interactive plots from Python in a Jekyll blog
---
# Interactive plots
I've been trying for awhile to get interactive plots going on my Jekyll blog. It turns out you can export plots from `matplotlib` in Python to HTML using a handy library called [`mpld3`](https://mpld3.github.io/). I'll write more about the details later, but for now I just wanted to show off one of my first interactive plots!

## Splitting up rap and country
After [analyzing 12k+ country lyrics](http://www.johnwmillr.com/trucks-and-beer/), I've gone and downloaded 25k+ rap lyrics using my [LyricsGenius](https://github.com/johnwmillr/LyricsGenius) python wrapper. I'm still working on my analysis of those lyrics, but I think this first plot is pretty funny. Rap artists are **much** more likely to use the word *like* in their songs. There is a clear separation on gender between country artists for the word *love*, but the effect doesn't appear to hold with rap artists.

{% include plot_like_love.html %}

## Up next
I'd love to make the plots even more interactive. It would be very cool if users were able to change the terms displayed in the plot. If anybody knows a way to do this with a Jekyll blog, let met know!