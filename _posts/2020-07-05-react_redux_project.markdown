---
layout: post
title:      "React/Redux Project"
date:       2020-07-06 03:55:09 +0000
permalink:  react_redux_project
---

For my last project, I adapted and expanded my previous javascript project to use the React framework and Redux state management library. The idea of the web application is to provide a more geographically focused exploration of the biodiversity observations from the website iNaturalist. I was primarily interested in being able to quickly show the distribution of observations/organisms across the United States at the state and county level while filtering by taxonomic classifications. All the iNaturalist data used in the project was obtained from the Global Biodiversity Information Facility, which provides open access to a massive amount of biodiversity data that has been parsed and homogenized under their data standards.

One of the biggest difficulties of this project was wrangling the large datasets throughout the different phases and components of the project. The following are a couple things I found particularly helpful to deal with that.

* csvkit - A command line tool for working with tabular data which was immensely useful to inspect, cut, and ultimately help import the csv data into a staging database where it could be worked with much more easily.

* react-window - Provides components for efficiently rendering large lists/tabular data. Rather than render an entire list/tabular dataset up front, only what is needed by the viewport is rendered at any given time. In my project, I had very large selection/search lists with up to 20,000 items. Using components with such large lists was extremely sluggish during selection/search/filtering, but using React-windowed-select pretty much eliminated this problem entirely.
    
* TopoJSON - Eliminates redundancy in how geographic data is stored in GeoJSON format. Rather than a file with discrete geometries and edges that are piled over each other, TopoJSON stiches those geometries together with shared line segments. This allows for much faster rendering, particularly when used with the improved geometry simplification/generalization the format provides.
    
In addition to issues with the large datasets, I occasionally ran into problems using React and D3 together. Since both React and D3 want control of the DOM and what is added/removed/altered based on data changes, there were times where components didn't function as expected. While there are many ways utilize them together, the way I found most intuitive (outside of React hooks) was to avoid the enter-update-exit pattern of D3 in favor of giving React the DOM control. For example, rather than having D3 append the svg map boundaries to a node of the DOM, I let react create the svg elements, and used D3 to grab the existing elements created by React to incorporate transitions and additional functionality.

Overall I felt that React/Redux made the implementation of the idea I was pursuing in the earlier Javascipt project much easier and far less flimsy. The state management of React/Redux allowed for a more solid and structured approach that meant it didn't feel like every change in my code would cause a cascade of problems. I'm looking forward to digging deeper into React in the future, particularly the use of hooks and how they can help in the use of D3.
