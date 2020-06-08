---
layout: post
title:      "Javscript/Rails Project"
date:       2020-06-08 01:41:24 +0000
permalink:  javscript_rails_project
---


For my javascript/rails API project I made an application to show the geographic distribution of biodiversity observations from [iNaturalist](https://www.inaturalist.org). iNaturalist keeps a large database of user contributed, community identified organism observations for all forms of life and shares those observations with the Global Biodiversity Information Facility (GBIF). GBIF processes, curates, and provides open access to a wide range of datasets about all types of life on earth, including iNaturalist observations. The basic idea of the application was to provide a more geographically focused method to browse the observations and see how organisms were distributed throughout the United States on a county or state level. To do this, the application uses three main components on top of the base rails api and javascript frontend.

* PostGIS - a spatial extension for PostgreSQL that adds support for geographic objects and spatial queries.
* RGeo - a geospatial data library for ruby that allows for the creation of geographic ojects (which can be stored and manipulated in a PostGIS extended database).
* D3.js - a javascript library that provides an extensive framework for interactive data visualizations.

The application allows for a user to view the geographic distribution (state or county) of total observations of organisms by kingdom, phylum, class, order, family, genus, species, or common name. Users can click on a county or state within the map to view a table of the most recent observations of the query results within that geographic boundary.

![](https://raw.githubusercontent.com/mattted/mattted.github.io/master/img/geodiv.png)

One of the biggest difficulties of this project for me was trying to maintain proper object oriented principles and keeping well organized code. If I'm being honest, I think I feel a little short on both accounts. After pretty much every project I find myself thinking that I should have spent more time planning, despite the fact that I did spend quite a bit of time planning the structure of each project. I think it boils down to the fact that planning can only help to a certain extent without a really solid understanding of the design patterns needed for each language or project. While getting a solid grasp on the structure, syntax, and details of a language are obviously extremely important, I think I learn the most from these projects by being able to look back at the end and identify the situations in which certain designs/patterns were succesful or unsuccessful.
