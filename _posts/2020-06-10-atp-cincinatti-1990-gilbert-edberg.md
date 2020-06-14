---
toc: false
layout: post
description: With tennis tournaments being suspended, I spend some time to create event data for a historical match - the ATP final in Cincinatti where Brad Gilbert faced Stefan Edberg. Here are some stats about the match you may have not seen before.
categories: [tennis analytics, atp tour, event data, Cincinatti, Brad Gilbert, Stefan Edberg]
title: A data-driven analysis of ATP Tour Final in Cincinatti in 1990 - Brad Gilbert vs. Stefan Edberg
image: images/cincinatti1990/Movement_EdbergServe.png
---
## Introduction
Recently my brother finally read Brad Gilbert's [Winning Ugly (1993)](https://www.amazon.com/Winning-Ugly-Mental-Warfare-Tennis-Lessons/dp/067188400X/). I tried to convince him for quite some time that he should read it but he ignored my advice for a long time. He proposed that I should create some event data for one of Brad Gilbert's matches. With all tennis tournaments being suspended at the time I thought that this might be fun. So, I went to TennisTV and typed "Brad Gilbert" into the search box and got exactly one result: The [ATP Final in Cincinatti](https://en.wikipedia.org/wiki/1990_Thriftway_ATP_Championships_%E2%80%93_Singles) where Brad Gilbert faced Stefan Edberg. As creating event data basically means to note the location of each bounce and hit on the court, I was quite pleased that the match was a fast 6:1 6:1 victory of Stefan Edberg, even though Brad Gilbert won't agree with me on this. :) 
The biggest challenge for the data collection was that I had to write a tool that allows me to collect the hit and bounce information independent of the camera image because a significant part of the match was not shown in this nice static topview that is used today. I spare you with the details of the collection, and let's focus on why it is pretty cool to have event data for this match.

## Event Data
To start with, here is a simple visualization what event data is. We record different events in the match and for each we note the position of the event and the position of each player at the time of the event. 
![Tennis Event Data]({{ site.baseurl }}/images/cincinatti1990/TennisEventData.png "An example of a rally captured with event data.")
In the example, Edberg is serving from the right, we record the positions of Gilbert, Edberg and the ball at the time of the serve (S), each time the ball bounces (B) or a player hits (H) the ball and when the rally is finished (P). This allows us to investigate a match on a rally or even single-event level that is clearly way out of scope for common box statistics.

## Stats
As this match happened 30 years ago we only have box score statistics of it. If you are interested, [here](https://tt.tennis-warehouse.com/index.php?threads/match-stats-report-edberg-vs-gilbert-cincinnati-final-1990.646293/) is a more in-depth discussion of the match.
But, box scores do not tell the whole story of a match and I believe that you can get so much more insights based on player and ball movement compared to these simple summary statistics. Therefore, I wanted to provide at least some insights based on statistics that are not available with simple box scores.

### Rally breakdown
Let's start with something simple that should be part of every analysis. A breakdown of all winners and errors over the rally length.
[Craig O’Shannessy](https://www.braingametennis.com/) is a big advocate for this kind of analysis, and I agree that this makes total sense. You need to put statistics into context and a breakdown by rally length let you easily spot where you lost or won the points.
Therefore, lets look at the winners and errors of Edberg and Gilbert and split them into rallies of lengths 0-4, 5-8 and 9+.  
  
| Player | Type  | 0-4 | 5-8 | 9+ |
|---|---|---|---|---|
| B.Gilbert | Winner  | 6  | 4  | 0  |
| B.Gilbert | Error  | 28  | 2  | 4  |
| S.Edberg | Winner | 15 | 3  | 0  | 
| S.Edberg | Error | 16 | 1  | 0  |
  
  
What we can see is that Edberg managed to keep the rallies short, especially through his serve&volley game. He hit a lot winners with his first strokes and also forced Brad Gilbert to play tough shots which resulted in a lot of errors early in the rallies.
Nowadays, [Craig O’Shannessy](https://www.braingametennis.com/) is advocating that players should come to the net more often and that one should focus more on playing the points in 0-4 smart. Therefore, Edbergs game plan in this final might be a blueprint of what O'Shanessy wants the game to look like. Lets look at the stroke distribution of both players.

### Stroke Breakdowm
The distribution of strokes for both players is a statistic that is also available with box scores. It clearly shows that Edberg varied his strokes more than Gilbert and managed to play lots of volleys.
![]({{ site.baseurl }}/images/cincinatti1990/StrokeDistribution_wide.png "Stroke distribution: Edbergs varies his strokes a lot.")
Building on this we can look at the first stat that is not available without event data. The **covered distances** of both players.

### Covered distances
When you have the hit locations of all strokes of a player and the player positions, it is simple to calculate the distance he covered during a rally and the match. Here are the results for the match. You might have guessed that Gilbert runs more than Edberg, but actually Edberg managed to not let Gilbert run and actually covered more distance through moving to the net than Gilbert running all over the court chasing Edbergs volleys.

![Covered Distances]({{ site.baseurl }}/images/cincinatti1990/DistanceCovered.png "Distance covered: Edberg managed to not let Gilbert move a lot.")


### Serve locations and next stroke
We have seen that Edberg played a lot of serve&volley, thus it is interesting to look into his serve locations and follow up strokes.
Here is a breakdown of all serve locations and positions of Edbergs next stroke. (Only including points where Edberg actually had to hit the second ball.) Ball bounces are colored yellow and the hit positions of Edbergs first stroke after the serve are colored red and green indicates if Edberg won this point or not. The hit positions show that Edberg played serve and volley almost every time and did this very successfully.

![]({{ site.baseurl }}/images/cincinatti1990/Edberg_ServeAndVolley.png "Serve and volley locations on S.Edberg's serve")


### Movement Radars
When you have the positions of each player at each bounce and hit event, it feels quite natural to ask if one could use this information to get more insight into the actual movement of the players. Labeling each event in the match I recognized that S. Edberg was moving a lot forward to the net, especially given his exclusive serve&volley strategy. On the other hand, B. Gilbert was not moving a lot, as shown before, and his movement was more left and right around the baseline, especially when S. Edberg was serving.
Let's investigate the movement of both players for B. Gilberts service games.  
Instead of showing a heatmap I want to try something else and create **movement radars** to quantify the movement directions for each player. The intuition is that we should be able to see if someone was coming to the net often or just running left to right. If someone was forced to only play backhands this should also be visible. For each hit event I note down the covered distance and the relative angle between the current and the last position of the player. Then I split the movements into eight equidistant intervals create a simple histogram.  
Sounds complicated? Lets look at the results.

![]({{ site.baseurl }}/images/cincinatti1990/Movement_GilbertServe.png "Movement radars when B.Gilbert served")
Here are the movements of Gilbert and Edberg in Gilberts serve. We can see that Gilbert was moving forward and comming to the net often and that Edberg forced him to play backhand ground strokes and volleys. Edberg, on the other hand, was moving left and right and hitting forhand and backhands but also moved forward to the net when he had a change to do so. I think that this "simple" chart can tell you a good story about the match. Lets look at the movements when Edberg was serving.


![]({{ site.baseurl }}/images/cincinatti1990/Movement_EdbergServe.png "Movement radars when S.Edberg served")
We can clearly see that Edberg was moving forward and playing serve&volley a lot. Furthermore, he played mostly backhand volleys and acted cross-court. Also, Edberg played to Gilberts backhand a lot and made him move to ad-court and sometimes even backwards.  
Additionally, lets focus on the annotations in each part of the pie. These are distances covered for each of the eight angles. You can clearly see how Edberg covered a lot more distance coming to the net than Gilbert running right to left on the baseline.


## Summary
Overall I hope that I could show the value of event data in tennis and there is so much more you can do with this kind of data. I think you can nicely see how Edberg, on top of his game in 1990, forced Gilbert to play where he was incredibly good at - focusing on short rallies and finishing at the net. In the final 1990 Edberg was playing his strengths to his opponents weaknesses, in principal following the future advice in [Winning Ugly](https://www.amazon.com/Winning-Ugly-Mental-Warfare-Tennis-Lessons/dp/067188400X/) (released in 1993) to the point.

