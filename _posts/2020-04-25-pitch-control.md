---
toc: false
layout: post
description: I show how you can run William Spearmans Pitch Control model implemented by Laurie Shaw directly in Google Colab. No instalation needed, it just works.
categories: [friends of tracking data, FoTD, Google Colab, tracking data, metrica sports]
title: One click to Pitch Control - Running Spearmans Pitch Control model in Google Colab.
image: images/PitchControl_Colab.png
---
The content the guys from Friends Of Tracking Data ([#FoT](https://twitter.com/hashtag/FoT?src=hashtag_click)) are putting out there is growing and recently [Laurie Shaws](https://twitter.com/EightyFivePoint) shared his implementation of [William Spearman's]((https://twitter.com/the_spearman))pitch control model from 2018. Also recently [Devin Pleuler](https://twitter.com/devinpleuler) shared his [Analytics Handbook](https://github.com/devinpleuler/analytics-handbook) which consists of a bunch of jupyter notebooks that you can run directly in [Google Colab](https://colab.research.google.com/notebooks/intro.ipynb#recent=true). This means you do not need to install anything, using the code is just one click away. I think that every repository should be build in this way as you won't have any overhead if you just want to play around.  
I thought it would be really cool to also be able to just run Spearman's Pitch Control model in this way. Therefore, I've restructured Lauries repository to allow for direct Google Colab integration.  

| Notebook | Colab |
| ------ | ------ |
| [Basic Plotting of Event and Tracking Data](https://github.com/seidlr/LaurieOnTracking/blob/master/notebooks/Lesson4.ipynb) | <a href="https://colab.research.google.com/github/seidlr/LaurieOnTracking/blob/master/notebooks/Lesson4.ipynb" target="_blank" ><img src="https://colab.research.google.com/assets/colab-badge.svg></a> |
| [Advanced Plotting and Summary Statistics]((https://github.com/seidlr/LaurieOnTracking/blob/master/notebooks/Lesson4.ipynb) ) | <a href="https://colab.research.google.com/github/seidlr/LaurieOnTracking/blob/master/notebooks/Lesson5.ipynb" target="_blank" ><img src="https://colab.research.google.com/assets/colab-badge.svg></a>|
| [Pitch Control](https://github.com/seidlr/LaurieOnTracking/blob/master/notebooks/Lesson6.ipynb) | <a href="https://colab.research.google.com/github/seidlr/LaurieOnTracking/blob/master/notebooks/Lesson6.ipynb" target="_blank" ><img src="https://colab.research.google.com/assets/colab-badge.svg></a>|
{: #colab}  

   You can get the code on Github: [https://github.com/seidlr/LaurieOnTracking](https://github.com/seidlr/LaurieOnTracking)

Just click on the `Open in Colab` batch next to Pitch Control and you are good to go. Then:
- Run each cell in the notebook and ignore the warning about the unknown environment.
- The data is downloaded directly from Metricas repository.  
- Give it some time when it says "Reading team home" in a cell.  

![Pitch Control in Google Colab](https://i.imgur.com/VwiiBtm.png)

If you are interested in the details what I needed to change to be able to run the code in Google Colab, you can find all code in my fork of Lauries repository on [Github](https://github.com/seidlr/LaurieOnTracking). Here are the new benefits.
- A clean structure, where notebooks and modules are separated.
- The Metrica sample data is directly read from their github repository.
- You can run the notebooks directly in Google Colab.
- It is pip-installable. Just run 
```
pip install git+https://github.com/seidlr/LaurieOnTracking.git
```
And you are able to use the implementation anywhere in your projects. I.e. you can read in the metrica data of sample match 2 in a dataframe with this code snippet.
```
import friendsoftracking.metrica.IO as mio
game_id = 2 # let's look at sample match 2
# read in the event data
events = mio.read_event_data(game_id)
events.head()
```

