---
layout: page
title: Projects
category: project
image: assets/images/pies.jpg
---

<h1 class="title">{{ page.title }}</h1>

<section class="list">

</section>

Most of my work is on [GitHub](https://github.com/johnwmillr), [Instructables](https://www.instructables.com/member/johnwmillr/), and [/r/DataIsBeautiful](https://www.reddit.com/r/dataisbeautiful/search?sort=top&q=author%3A%22textureflow%22+title%3A%5BOC%5D&restrict_sr=on).

---

## DataIsBeautiful
[![dataisbeautiful](https://s3.amazonaws.com/freebiesupply/large/2x/reddit-logo-png-transparent.png){:class="img-responsive" height="20%" width="20%"}](https://www.reddit.com/r/dataisbeautiful/search?sort=top&q=author%3A%22textureflow%22+title%3A%5BOC%5D&restrict_sr=on)

I am a regular contributor to [/r/DataIsBeautiful](https://www.reddit.com/r/dataisbeautiful/search?sort=top&q=author%3A%22textureflow%22+title%3A%5BOC%5D&restrict_sr=on), a data visualization community on Reddit. A few of my posts have been quite popular on the site, collectively receiving more than a million views. You can take a look at the list of all of [my posts](https://www.reddit.com/r/dataisbeautiful/search?sort=top&q=author%3A%22textureflow%22+title%3A%5BOC%5D&restrict_sr=on) or check out one of the popular ones below:
 - [Words per song for rap, rock, and country music](https://www.reddit.com/r/dataisbeautiful/comments/8j1r7b/words_per_song_for_rap_rock_and_country_music_oc/)
 - [The average faces of rap, rock, and country musicians](https://www.reddit.com/r/dataisbeautiful/comments/crxrud/the_average_faces_of_rap_rock_and_country/)
 - [Funding probabilities on Shark Tank, grouped by gender](https://www.reddit.com/r/dataisbeautiful/comments/8wr8ko/funding_probabilities_on_shark_tank_grouped_by/)
 - [Distributions of height for the different positions in the 2018 FIFA World Cup](https://www.reddit.com/r/dataisbeautiful/comments/8sg3ok/distributions_of_height_for_the_different/)

---

## Facer -- ***Summer 2019***

[![Facer GIF](/assets/images/FaceAverages/AverageFace_Apple.gif){:class="img-responsive" height="30%" width="30%"}](https://github.com/johnwmillr/Facer)

[Facer](https://github.com/johnwmillr/Facer) is a Python package I wrote that simplifies the process of creating [average face images](https://www.google.com/search?safe=active&q=average+face&tbm=isch&source=univ&sa=X&ved=2ahUKEwii_L76goHkAhUqwFQKHX83As4QsAR6BAgFEAE&biw=1440&bih=7). The package draws heavily from a preexisting tutorial written by [Satya Mallick](https://twitter.com/learnopencv). The majority of my work consisted of updating the tutorial's code to work with Python 3 and the latest version of OpenCV. I also added streamlined functions to go straight from a directory of images to an averaged face or animated GIF. I used Facer in a popular [Reddit post](https://www.reddit.com/r/dataisbeautiful/comments/crxrud/the_average_faces_of_rap_rock_and_country/), which in turn inspired other users' [posts](https://www.reddit.com/r/dataisbeautiful/comments/cx3pp6/oc_averaged_faces_of_members_of_the_116th_united/) on [Reddit](https://www.reddit.com/r/dataisbeautiful/comments/cxff61/oc_average_face_of_miss_daegu_2013_beauty_pageant/).

---

## SpoonacularAPI -- ***Summer 2018***
[![Build Status](https://travis-ci.org/johnwmillr/SpoonacularAPI.svg?branch=master)](https://travis-ci.org/johnwmillr/SpoonacularAPI)
[![PyPI version](https://badge.fury.io/py/spoonacular.svg)](https://pypi.org/project/spoonacular/)
[![Python version](https://img.shields.io/badge/python-3.x-brightgreen.svg)](https://pypi.org/project/spoonacular/)

[![Spoonacular Logo](/assets/images/spoonacular.png){:class="img-responsive" height="30%" width="30%"}](https://github.com/johnwmillr/SpoonacularAPI)

[Spoonacular](http://spoonacular.com/) is a food and recipe website that offers a freemium API with over fifty different endpoints. The API even includes endpoints for random [food jokes](https://twitter.com/johnwmillr/status/1027443472985452544) and [wine pairings](https://twitter.com/johnwmillr/status/1025989502957969408)! I developed [`spoonacular`](https://github.com/johnwmillr/SpoonacularAPI), a Python package that interfaces with the Spoonacular API and makes it easy to download food, recipe, and nutrition data from the website. I wrote unit tests for each of the endpoints and have continuous integration running on [Travis-CI](https://travis-ci.org/johnwmillr/SpoonacularAPI). The package is available for installation via [`pip`](https://pypi.org/project/spoonacular/).

---

## SportradarAPIs -- ***Summer 2018***
[![Build Status](https://travis-ci.org/johnwmillr/SportradarAPIs.svg?branch=master)](https://travis-ci.org/johnwmillr/SportradarAPIs)
[![PyPI version](https://badge.fury.io/py/sportradar.svg)](https://pypi.org/project/sportradar/)
[![Python version](https://img.shields.io/badge/python-3.x-brightgreen.svg)](https://pypi.org/project/sportradar/)

[![Sportradar Logo](https://sportradar.us/wp-content/uploads/2015/12/logo-retina.png){:class="img-responsive" height="30%" width="30%"}](https://github.com/johnwmillr/SportradarAPIs)

[Sportradar](http://sportradar.com/) is a company that provides extensive APIs for a number of professional sports including soccer, basketball, and multiple eSports leagues. I wrote a [`sportradar`](https://github.com/johnwmillr/SportradarAPIs), a Python package that simplifies the process of downloading data from Sportradar's APIs. A fun part of the project was writing a [script](https://github.com/johnwmillr/DocScraper/blob/master/sportradar/scrapeSportradarEndpoints.ipynb) to scrape the Sportradar documentation and automatically generate functional Python code and unit tests for each API endpoint. My [analysis](/fifa-world-cup-data/) of data from the 2018 FIFA World Cup made use of `sportradar` and provides a few example use cases. The project is available via [`pip`](https://pypi.org/project/sportradar/).

---

## Automated medical diagnostics for retinal diseases -- ***Spring 2018***
[![Retinal layers](/assets/images/Fig_ILM.png){:class="img-responsive" height="23%" width="23%"}](https://ir.uiowa.edu/etd/6215/)

As part of my masters program at the University of Iowa, I worked as a research assistant in Dr. Mona Garvin's image processing lab. My research in Dr. Garvin's lab focused on the development of automated diagnostic tools for diseases of the retina. Specifically, I trained machine learning classifiers to use the characteristic shapes of retinal layers to differentiate between two types of optic disc swelling, [papilledema](https://en.wikipedia.org/wiki/Papilledema) and [NAION](https://en.wikipedia.org/wiki/Anterior_ischemic_optic_neuropathy). My research in the Garvin Lab culminated with a poster presentation at [ARVO 2018](https://iovs.arvojournals.org/article.aspx?articleid=2693706) and the defense of [my thesis](https://ir.uiowa.edu/etd/6215/).

---

## LyricsGenius -- ***Fall 2017***
[![Build Status](https://travis-ci.org/johnwmillr/LyricsGenius.svg?branch=master)](https://travis-ci.org/johnwmillr/LyricsGenius)
[![PyPI version](https://badge.fury.io/py/lyricsgenius.svg)](https://pypi.org/project/lyricsgenius/)
[![Python version](https://img.shields.io/badge/python-3.x-brightgreen.svg)](https://pypi.org/project/lyricsgenius/)

[![GeniusLogo](https://t2.genius.com/unsafe/220x0/https%3A%2F%2Fimages.rapgenius.com%2F716fe1fbbf4817447e21dd2f9aca0354.999x1000x1.png){:class="img-responsive" height="20%" width="20%"}](https://github.com/johnwmillr/LyricsGenius)

[LyricsGenius](https://github.com/johnwmillr/LyricsGenius) is a Python package I wrote that allows users to programmatically access lyrics, artist information, and song media from [Genius.com](https://genius.com/). Genius is a fun website that lets users upload song lyrics and collaborate on annotations and interpretations of artists' words. I wanted a simple way to download lots of song lyrics at once, so I thought I'd write a Python wrapper for the API Genius provides. The code is hosted on [GitHub](https://github.com/johnwmillr/GeniusAPI) and can be installed using [PyPI](https://pypi.org/project/lyricsgenius/). I used LyricsGenius for my analysis of [country song lyrics](/trucks-and-beer/).

---

## Fivecircle -- ***Fall 2017***
[![Fivecircle](https://upload.wikimedia.org/wikipedia/commons/1/13/Zentao.png){:class="img-responsive" height="10%" width="10%"}](https://fivecircle.herokuapp.com/)

[Fivecircle](https://fivecircle.herokuapp.com/) is a geo-based social media platform I built with a five-person team as part of a software engineering course I took in the fall of 2017. The web app lets users post geo-tagged photos and notes for other users to view. We built Fivecircle using Ruby on Rails while following an Agile methodology and maintaining best practices on our GitHub [repository](https://github.com/johnwmillr/Fivecircle). We made use of the Google Maps API for geocoding as well as the devise ruby gem for authentication. [Sign up](https://fivecircle.herokuapp.com/users/sign_up) for an account and start sharing posts!

---

## Active shape models for face detection -- ***Spring 2017***
[![Faces](https://raw.githubusercontent.com/johnwmillr/ActiveShapeModels/master/Media/Video/ASM_FaceDetection_24-Jul-2017_MUCT.gif){:class="img-responsive" height="30%" width="30%"}](https://github.com/johnwmillr/ActiveShapeModels)

For the final project in my Advanced Digital Image Processing course, I chose to research and implement active shape models a technique originally developed by [Tim Cootes et al.](https://www.sciencedirect.com/science/article/pii/S1077314285710041) in 1995. My Matlab code trains a point distribution model from a manually-labeled set of images of faces and is then able to successfully locate faces in new images using the ASM technique. Check out my GitHub [repository](https://github.com/johnwmillr/ActiveShapeModels) for a complete description of the project.

---

## EMG audio amplifier -- ***Spring 2017***
[![EMGaudio](https://content.instructables.com/ORIG/FSY/V1BE/J47LCT82/FSYV1BEJ47LCT82.png?auto=webp&frame=1&width=982&height=1024&fit=bounds&md=158fe3c05468134ed9e32e87929b4372){:class="img-responsive" height="30%" width="30%"}](http://www.instructables.com/id/Build-a-Muscle-Audio-Amplifier-Electromyography)

During the spring of 2017 I built an electromyography (EMG) audio amplifier. The two-channel device was built from analog integrated circuit components (op-amps, instrumentation amps, and audio amps), included band-pass filters, and could output audio through a standard 1/8" audio jack. Visit the link for images and schematics of the device as well as detailed instructions for building your own. After I published my project to the Instructables website the HackADay blog [featured](https://hackaday.com/2017/06/24/listen-to-your-body) my work and Tweeted a link out to their 100K+ followers!

---

## Muscle-controlled MIDI device -- ***Winter 2017***
[![MIDImuscle](https://content.instructables.com/ORIG/F7A/0QZB/IYKFXBWB/F7A0QZBIYKFXBWB.png?auto=webp&frame=1&width=1024&height=1024&fit=bounds&md=a401ea8cb83d38921cfb19d631938002){:class="img-responsive" height="30%" width="30%"}](http://www.instructables.com/id/Make-Muscle-MIDI-Music/)

During the winter of 2017, I built an electromyography ([EMG](https://en.wikipedia.org/wiki/Electromyography)) amplifier which allowed users to trigger MIDI instrument sounds (e.g. a snare drum) by flexing their muscles. The device used muscle activity as a control signal for both volume and pitch of the MIDI notes. After the muscle activity was amplified and filtered via a custom-built analog circuit, an Arduino translated the EMG signals into MIDI signals which were then sent over Bluetooth to an iPhone running Garageband. I ended up winning second prize in the [Instructables Sensors 2017 contest](http://www.instructables.com/contest/sensors2017/).

---

## Halloween drum machine costume -- ***Fall 2016***
[![MIDIcostume](https://content.instructables.com/ORIG/F30/YA8B/J44FX9TH/F30YA8BJ44FX9TH.png?auto=webp&frame=1&width=533&height=1024&fit=bounds&md=b53f642bdae67dac7fbe7ee5961a1d77){:class="img-responsive" height="22%" width="22%"}](http://www.instructables.com/id/Functional-MIDI-Drum-Machine-Costume)

For Halloween 2016 I designed and built a fully functioning MIDI drum machine costume. The costume consisted of piezoelectric sensors worn on the chest which sent signals into an Arduino when tapped. I wrote code for the Arduino that translated the raw force signals into MIDI commands which were sent to an iPhone running GarageBand. The iPhone then played drum noises (triggered by the sensors on my chest) through a Bluetooth speaker. I wrote a description of the project along with a step-by-step tutorial for [Instructables](http://www.instructables.com/id/Functional-MIDI-Drum-Machine-Costume).

---

## Musician Maker -- ***Summer 2011***
[![Guthman](https://www.goshen.edu/wp-content/uploads/sites/2/2012/02/Guthman2012.jpg){:class="img-responsive" height="22%" width="22%"}](https://www.goshen.edu/academics/2012/02/29/miller-and-buschert-finalists-in-guthman-competition/)

During the summer of 2011 I worked on the "Musician Maker" project as part of Goshen College's [Maple Scholars Program](https://www.goshen.edu/academics/maple-scholars/). Musician Maker is an intuitive, computer-controlled system of novel instruments that allows non-musicians to improvise expressive music. During the winter of 2012 my advisor and physics professor, Dr. John Buschert, and I competed in and were selected as finalists for the [2012 Guthman New Musical Instrument Competition](https://www.youtube.com/watch?v=5YQF2KTMRPs) hosted at Georgia Tech. I wrote multi-threaded Python code that generated artificial music and interfaced with the novel hardware instruments.
