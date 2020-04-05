---
layout: post
title:      "Sinatra MVC Project: Planted"
date:       2020-04-05 05:34:27 -0400
permalink:  sinatra_mvc_project_planted
---


For my Sinatra project I chose to make a simple plant collection application that allows users to add plants, log events for watering and fertilizing, and track scheduling for each. The model relationships for the application were pretty simple and straighforward with 5 total models (visualized below using rails-erd gem)
![erd](https://raw.githubusercontent.com/mattted/mattted.github.io/master/img/Planted%20ERD.png)

The basic flow of the application is that a user will add a plant with general information, decide whether to set a static schedule or one that changes based on watering/fertilization history, and add water / fertilizer events as they happen or retroactively. When enough water/fertlizer events are recorded, the next water or fertilizer date will be suggested based on an average of previous events or by the static schedule set by the user.
Other general functionality:
* View general plant information individually or in a table with all of users plants
* View all water or fertilizer events for a user, or view by individual plant
* Edit all plant information, including shifting to or from static or averaging schedules
* Add/delete water or fertilizer events for an individual plant or for many at once (updating scheduling when added/deleted)
* Delete plants and all associated logs/tracking information records.



### Difficulties

One of the issues I had when coding this project was maintaining what felt like proper RESTful routing conventions. In the early stages without many routes, it felt pretty clear cut and I probably didn't give it quite enough thought. Once I was towards the end of the project with numerous routes, many with overlapping themes/content, I had a little more trouble maintaining seemingly sensible routes without some requests accidentally getting improperly routed. It's certainly something I will be more cognizant of when working on a project like this again.

Another issue I generally have is planning through the conceptual phases of projects early on. I tend to get too bogged down in how exactly the structure of the project (models, views, controllers, routes, helpers etc) should look at completion rather than building incrementally as I go. At least for me, trying to produce too much of the structure early on can lead to a overly rigid approach to getting the functionality I want. I feel like finding a balance between following an initial plan/structure while allowing a flexible and fluid approach to problems as they arise is a skill that will be exceptionally important to hone as I work through this course.









