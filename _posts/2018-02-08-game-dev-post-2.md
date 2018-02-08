---
layout: default
title:  "Game Dev - Post 2"
date:   2018-02-08 12:00:00
categories: gamedev
---

# Game Dev - Post 2

I started on another tutorial series, this time for a tower defense game ([link](https://www.youtube.com/watch?v=beuoNuK2tbk&list=PLPV2KyIb3jR4u5jX8za5iU1cqnQPmbzG0)). This tutorial is much more involved than the last game, as well as a fair amount longer. I've gotten to the point where I am working with pre-made assets. One aspect of this tutorial series that has been slightly frustrating has been the path creation for the enemies to follow. I wasn't sure if everything had to be pixel perfect or not, which made things quite time consuming. Using pre-made assets has me excited to start trying out modifying existing assets or creating my own. Another thing that I thought was very interesting was how simple basic waypoint creation was. Making the waypoints and having the enemies follow them was much easier than I originally anticipated. The gist of the creation is:

- Have an array of waypoints in a defined order from start to finish.
- Tell your enemy to move toward the first point.
- Once the enemy gets within a certain distance to the point, move to the next point.
- Rinse and repeat until the enemy gets to the end.
- Delete the enemy (which will later count against a total score, player health amount, etc.)

There is still a lot to learn with this tower defense tutorial, but I am looking forward to digging deeper into it!