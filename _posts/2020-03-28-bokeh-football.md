---
toc: false
layout: post
description: How to create an interactive football plot for tracking data with bokeh server.
categories: [friends of tracking data, FoTD, bokeh, tracking data]
title: Visualising Football Tracking Data with Bokeh Server
image: images/bokeh-football.png
---
Last Thursday I listened to the first episode of [Friends of Tracking](https://www.youtube.com/channel/UCUBFJYcag8j2rm_9HkrrA7w) where David Sumpter
([@Soccermatics](https://twitter.com/Soccermatics)), [@JaviOnData](https://twitter.com/JaviOnData), [@AlexThomasTheFA](https://twitter.com/AlexThomasTheFA), [Suds Gopaladesikan](https://www.linkedin.com/in/sudarshan-gopaladesikan-24321a29/), [@PeraltaFran23](https://twitter.com/) and [@pascal_bauer](https://twitter.com/pascal_bauer) had the great idea to "give back during difficult times". They will provide open lectures on football analytics explaining how they work inside clubs and national teams on their [Youtube channel](https://www.youtube.com/channel/UCUBFJYcag8j2rm_9HkrrA7w). As the name of their group suggests the group was initiated when tracking data became available in football and they recognized that everyone was working on the same problems and code. Because David Sumpter also mentioned that he tries to get some free tracking data of the Swedish league I thought that it might be a good idea to share a repository I found that can be used to easily visualize tracking data in a Jupyter notebook and start from there instead of implementing the visualization. It is written in Python and uses [bokeh](https://docs.bokeh.org/en/latest/index.html) for the interaction. The nice thing is that it already has features to show Voronoi cells and convex hulls of both teams.

You can find the code at [https://github.com/seidlr/Game-Animation](https://github.com/seidlr/Game-Animation) and follow the instructions in the `Readme`.  
Here is a short summary if you already have Anaconda installed:
1. Clone the repository
```
git clone https://github.com/seidlr/Game-Animation
```
2. Change the directory
```
cd Game-Animation
```
3. Create the conda environment
```
conda env update
```
This creates a conda environment called `game-animation`.
4. Activate the environment
```
conda activate game-animation
```
5. And finally start the jupyter notebook server
```
jupyer notebook
```
6. Select the `Soccer_example.ipynb` and run the code cells.

Following the instructions in the notebook you can easily visualise and animate tracking data. It might look like this:
<script
    src="https://bokeh-football.apps.talksportsdata.com/bokeh-football/autoload.js?bokeh-autoload-element=1000&bokeh-app-path=/bokeh-football&bokeh-absolute-url=https://bokeh-football.apps.talksportsdata.com/bokeh-football"
    id="1000">
</script>

Using the code you can actually focus your time on more valueable projects than building the visualisation. Here are some ideas to get started.

## Possible extensions
- Color the Voronoi cells by team in red and blue.
- Use `sklearn` K-means on the `x` values to find three clusters for attack, midfield and defense.
- Draw lines between the players in each of the clusters as shown [here](https://twitter.com/spielvercom/status/1243957222876614657?s=20):
![Lines between players in clusters](https://i.imgur.com/gvM7rwX.png)
- Count all "line-breaking" passes

# Note
I have just forked this repository from `https://github.com/samirak93/Game-Animation`. The code was not written by me. I only made some small changes to make it easier to use:
- I've cleaned up unneccesary folders like `__pycache__` and `.ipynb_checkpoints`.
- I've added a `.gitignore` file to keep the repository clean.
- I've added an `environment.yml` file such that you can install all necessary requirements to run the notebooks.
- I've changed the calculation of the convex hull of teams to not include the goalkeeper.  








![](assets/2020-03-28-19-24-04.png)

