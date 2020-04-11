---
toc: false
layout: post
description: How to create an interactive football plot for tracking data with bokeh server.
categories: [friends of tracking data, FoTD, widgets, bqplot, qgrid, tracking data, metrica sports]
title: An Interactive Visualisation of Football Tracking Data.
image: images/fotd_widgets_thumbnail.png
---
# An Interactive Visualisation of Football Tracking Data
Unfortunately, I missed the last episode [How Tracking Data is Used in Football and What are the Future Challenges of Friends of Tracking Data](https://www.youtube.com/watch?v=kHTq9cwdkGA) hosted by David Sumptor ([@Soccermatics](https://twitter.com/Soccermatics)) with [@JaviOnData](https://twitter.com/JaviOnData), [@the_spearman](https://twitter.com/the_spearman), [Suds Gopaladesikan](https://www.linkedin.com/in/sudarshan-gopaladesikan-24321a29/) and [@EightyFivePoint](https://twitter.com/EightyFivePoint). It felt a bit like missing a great panel at a conference due to overlap in schedules. Luckily for me, and all others, everything is recorded on Youtube and available [here](https://www.youtube.com/watch?v=kHTq9cwdkGA). This is what David had to say about the episode.

{% twitter https://twitter.com/Soccermatics/status/1248614585851998214?s=20 %}

I agree one hundred percent that it was a really in-dept discussion of current issues. They also managed to get sample tracking data of two matches from [Metrica Sports](https://github.com/metrica-sports/sample-data). Given the quality of the talk they had, I thought I will have to up the ante on my side. I thought about what I would have been very happy to know a year ago and therefore I created a notebook where I use Jupyter widgets the create interactive components which you can use to investigate the Metrica Sports data. You can get all the code on Github, [https://github.com/seidlr/fotd-interactive-football-pitch](https://github.com/seidlr/fotd-interactive-football-pitch), and simply follow the installation instructions in the Readme.  
Or, and this is what I really like about Jupyter widgets, you can just use Binder to test everything online without installation.   
Just click on this image   
<center>
<a href="https://mybinder.org/v2/gh/seidlr/fotd-interactive-football-pitch/master?filepath=Interactive-Football-Pitch.ipynb" target="_blank" ><img src="https://mybinder.org/badge_logo.svg"></a>
</center>
(and give Docker some time to build the image)

Here are some screenshots of the three use-cases I picked as showcases:
##  Use-case 1: Moving Players on a Football Pitch
I think everyone will share kind of the same story of how his or her visualisation of football pitches changed or improved over time. For me it was starting with Matplotlib and switching to Plotly because you actually don't want to spent a ton of time to get some simple hover effects etc. But at some point you recognize that in the end you want to be able to actually move players or the ball around on the pitch and possibly rerun your pitch control or expected-goals model and answer some What-If questions. If you reached this point, you will be pleased to see that this is actually possible using `bqplot`, a Python wrapper around D3.js, in a jupyter notebook. If you launch the notebook on Binder, you can drag and drop each player and the ball on the pitch.

<center>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Kx9IY_HAkK8" frameborder="0" allowfullscreen></iframe>
</center>


## Use-case 2: Animate Tracking Data
The cool thing is that you can build our widgets on top of this in a simple way. As example I've attached a `Play` and `slider` widget. Now you can easily replay the match using tracking data.

<center>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/giqCwm85NzY" frameborder="0" allowfullscreen></iframe>
</center>


## Use-case 3: Replay Events with Tracking Data
The Metrica data also gives you access to all the events that happened in the match. Would be cool to be able to filter events and jump to the position in the replay where they happened? We can use a `qgrid` widget to do this! Here is the result.

<center>
    <iframe width="560" height="315" src="https://www.youtube.com/embed/RhDjOxW_qrY" frameborder="0" allowfullscreen></iframe>
</center>

## What to do from here?
Getting all the widgets into a state to run smoothly is always a bit challenging, especially because they tend to fail silently, meaning that there might be no error in the notebook but the widget is not doing what you want it to do because you made a mistake somewhere. The only way to learn how to use them is actually to invest time. The best way is to build on a widget and try to add new functionality.  
Here are some ideas:
- Add the current game time to the pitch plot (and update it when playing).
- Add some functionality like voronoi cells or convex hulls of teams as implemented [here](https://github.com/seidlr/Game-Animation).
- Add a auto-replay option: When selecting an event, the animation should start at this event and stop of it is over as documented in the columns `End X` and `End Y`.
- Create an overlay/tooltip for player information using `bqplot.tooltip`.
- Calculate the distance covered for each player and the ball in the match.
