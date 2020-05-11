---
layout: post
title:      "Rails Project: StatCaddie"
date:       2020-05-11 02:59:14 +0000
permalink:  rails_project_statcaddie
---


For my rails project I made a golf logging application that allows users to create courses, log rounds on on specified courses, and keep track of stats by round/course/hole etc. The general premise is that users create courses with course and hole specific information (yardage, par, tees) and all users can then log rounds on those courses. The relationships between all the models are pretty conventional, with the possible exception of the users/courses. Since users have many courses, both that they've created and through rounds, the foreign key and class names had to be specified to make distinct relationships. The diagram below shows the model relationships (generated with rails-erd gem)

![](http://raw.githubusercontent.com/mattted/mattted.github.io/master/img/statcaddie_erd.png)

One of the biggest difficulties I faced during the creation of this project was calculating stats for users and queries taking a long time to execute. Both issues can partially be attributed from my decision to make the statistical calculations for the models within instance methods, rather than saving them as attributes within the database. Initially this seemed to be a pretty clear cut choice. Instance methods were much more straight forward and calculations in methods could be constructed from a smaller set of attributes that would be stored in the database and accessed only when available. While this made things easier for dynamically calculating stats on active record instances, it made it impossible to use these in queries since they're not persisted to the database. Rather than fast active record/database query methods, I had to cut out of queries to interate over all the instances returned, run a calculation on each, conditionally map it to a new array, filter/order/aggregate, and then extract the information I needed.

Another aspect of the project that I don't think I planned correctly was how closely related some models should be, for example the Hole and Scorecard models from the entity relationship diagram above. Initially, when trying to make calculations on the scorecard model, I nearly always had to make a query to find the 'par' attribute of the associated hole (ie `scorecard.round.course.tees.where(some_condition).hole.where(some_condition).par`). In hindsight that seems pretty ridiculous but initially it made sense to me to just query for that attribute when I needed it rather than storing it as an attribute on the scorecard itself.

Both of the problems above were solved using a combination of the following:
* before_save methods to add stat attributes to tables at the appropriate times
* creating indexed lookup ids shared by models that need to have a closer relationship
* reducing iteration of, and calculations on, large collections of active record objects unless absolutely necessary
