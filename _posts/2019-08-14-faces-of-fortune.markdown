---
title: "Faces of Fortune 💰"
date: 2019-08-13
layout: post
tag:
 - python
 - data science
 - image processing
category: blog
author: john
name: john
image: /assets/images/FaceAverages/AverageFace_Apple.gif
description: "Faces of Fortune: The look of leadership at top US companies"
---

# Introduction

You've probably seen average faces before—they're not too [uncommon](https://www.google.com/search?safe=active&q=average+face&tbm=isch&source=univ&sa=X&ved=2ahUKEwii_L76goHkAhUqwFQKHX83As4QsAR6BAgFEAE&biw=1440&bih=766). The concept is simple: take a collection of pictures of faces and blend them together to create a single "average face" that is representative of the whole group. The actual blending process involves some complicated math, but it essentially boils down to aligning the faces to make sure the nose, eyes, mouth, etc. all line up.

I'd been playing with average faces for the last few weeks with—initially—only [amusing results](https://twitter.com/johnwmillr/status/1155707694063337472?s=20). After updating code from a slightly outdated (but extremely useful) [tutorial](https://www.learnopencv.com/average-face-opencv-c-python-tutorial/) and wrapping it into my own [Python package](https://github.com/johnwmillr/Facer), I was eager to find an application worth writing about.

{% include figure_link.html url="/assets/images/FaceAverages/Faces_RapRockCountry.png" href="/assets/images/FaceAverages/Faces_RapRockCountry.png" caption="Averages faces of female and male rap, rock, and country artists." width="60%" %}

After having [moderate success](https://www.reddit.com/r/dataisbeautiful/comments/crxrud/the_average_faces_of_rap_rock_and_country/) with averages of musicians' faces from different genres, my brother suggested I target a source where I could count on the composition of the photos being mostly consistent: Fortune 500 company executive leadership pages. So, the immediate goal of this post is simple: for each of the top 50 Fortune 500 companies, determine the average face of the company's executive leadership.

# Methods

## Downloading faces

I began by scraping the names of the top 100 companies on the [Fortune 500 list](https://fortune.com/fortune500/list). I used Selenium (an automated browsing tool) to load with the Fortune website and scrape the company names. Selenium is better suited than [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) for handling pages that use JavaScript, a feature I knew would more robustly handle individual company websites.

After collecting the [top 100 companies](https://github.com/johnwmillr/FacesOfFortune/blob/master/data/Fortune100.csv), I automated a Google search for each company: "*company name* corporate leadership page." For each searched, I saved the URL for the first hit from the same domain as the company website.

Next I scraped images from each company's corporate leadership page. This turned out to be more challenging than I expected. I was familiar with using BeautifulSoup to scrape images from websites, but simply finding all the `<img>` tags wasn't enough. For example, coming up with a specific solution for [Apple](https://www.apple.com/leadership/) would have been easy enough, but the method would be no good for me if it didn't work for all other websites on the list as well. I ended up with an approach that monitors all network traffic while Selenium loads a website and extracts and saves any image data.

Unfortunately, the fully automated scraping wasn't successful on about 15 of the top 50 websites. The most common issue was a corporate leadership page not including any images, only a list of names. For these websites, I ran Google image searches that included the individual and company's names and collected the first image to include a single face.

## Face averaging

Once corporate leadership images were downloaded for each company, I used my [Facer](https://github.com/johnwmillr/Facer) package to create the average faces. Facer is largely just a reworking of preexisting code from [Satya Mallick](https://twitter.com/learnopencv). The majority of my work was updating the tutorial's code for Python 3 and the latest version of OpenCV. Also, for some reason, installing OpenCV broke my Mac's Python install and virtual environments :( So watch out!

Point Facer at a directory of images and it:

  1. Detects faces in images
  2. Determines face landmarks locations (eyes, ears, mouth, etc.)
  3. Warps each face's landmarks to a standard central location (i.e. make sure each face is facing forward, toward the camera)
  4. Averages the overlapping faces together into a single image

{% include figure_link.html url="/assets/images/FaceAverages/AverageFace_Apple.gif" href="/assets/images/FaceAverages/AverageFace_Apple.gif" caption="Combining faces of Apple's executive leadership." width="90%" %}

# Fortune 500 (Top 50)
Well—as we might have guessed—the results are as unsurprising as they are uninspiring. I was expecting fifty images of mostly white men, but I didn't expect *just how similar* each of those images was going to appear. Apart from a handful of standouts (e.g. Target, Bank of America, Alphabet), I honestly thought I had made a mistake with my averaging code; how could I end up with so many *nearly identical* faces? Alas, the code's not the issue. Even when looking through company pages such as [General Motors](https://www.gm.com/our-company/leadership.html) where there are a few noticeable women or people of color, their appearance is quickly blended out by the overwhelmingly white male majority.

Take some time and look through the average faces for the top 50 companies. My favorite might be #25, Bank of America, a dead ringer for Mrs. Doubtfire.

[![Top 50 Companies]({{site.url}}/assets/images/FaceAverages/Top50.jpg){: .center-image }]({{site.url}}/assets/images/FaceAverages/Top50.jpg)

# Grouping by industry
The Fortune 500 list categorizes each company into an industry. After being a bit underwhelmed at the lack of *any* diversity when comparing each face in the top 50, I was curious whether we might see any trends when grouping the faces by industry. Would the average face of Finance appear older than the average face of Tech?

[![Industry faces]({{site.url}}/assets/images/FaceAverages/Industries.png){: .center-image }]({{site.url}}/assets/images/FaceAverages/Industries.png)

# Discussion
I hope this project inspires conversation. What questions does it bring to mind for you? Are these results interesting? Surprising? Useful? Important? What other areas could we apply this sort of work to? Let me know what you think!
