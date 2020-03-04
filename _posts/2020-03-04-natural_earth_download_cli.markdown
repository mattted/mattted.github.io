---
layout: post
title:      "Natural Earth Download CLI"
date:       2020-03-04 22:50:59 +0000
permalink:  natural_earth_download_cli
---


### Overview

The NaturalEarthDownload gem is a command line interface to download files from [Natural Earth Data](https://www.naturalearthdata.com). Natural Earth Data provides GIS vector and raster files with well integrated and maintained cartographic attributes to facilitate efficient map production. This gem was my attempt to provide an equally efficient way to download collections of that data and be able to save them to project specific folders without having to navigate through the website. The basic flow of the CLI is a user will follow prompts that will filter through the files by scale, type, category and theme --> add them to the download queue --> view a summary of file types and size within the queue --> download files from the queue to a folder of their choice.

### Structure

Since Natural Earth Data does not provide an API, all of the information needed to be scraped from the website using Nokogiri. I originally envisioned having a CLI class, Scraper class, File class, and Download Queue class; however, it quickly became apparent that I would need more classes in order to store information from the website as a user incrementally navigated through the CLI. Ultimately I ended up with the following classes:

* CLI - controls the flow of the program, calling on the Scraper class as new parts of the website need to be scraped and calls methods for getting input / displaying output.
* Scraper - scrapes the website and instantiates the appropriate instances of classes and their attributes. In order to keep from duplicating items, the scraper class only instantiates new classes when they don't already exist within the class's ::all method.
* DataTheme - the most generalized class. It holds all the data themes and scales
* DataVector - stores the name and description of vector files. Has a DataTheme.
* DataRasterCat - stores the name and description of raster categories. Has a DataTheme.
* DataRaster - stores the name and description of raster files. Has a DataRasterCat.
* Download - stores the name, size, description and download URL of the download. Has a DataRaster or DataVector
* DLQueue - has methods for listing and downloading files.

### Difficulties

For me, the hardest part of the CLI project was planning how to structure the classes and their relationships. When I first started writing the code, I was attempting to have each class carry a list of all the ways it related to the other classes. For example, when instantiating an instance of the most generalized class, DataTheme, I thought it would be best if that class would hold an array of each of the Download, DataRaster, DataVector, and DataRasterCat instances it would ultimately be related to and collaborating with. My thinking was that this would facilitate the easiest method of finding class instances of a certain type. If I wanted to get all the Download instances of a certain DataTheme I could just write something like `data_theme.downloads`. While that would be a quick way to access the downloads for a DataTheme, the implementation of relationships like that was overly complicated and unnecessary.

In the end I scrapped the code I had written and made much simpler relationships. Each class only related to one instance of another class, and held no arrays other than the instances of the class itself.  Changing class relationships greatly simplified how the classes collaborated. Since the Download class is at the deepest level of the relationship between classes and the one the user is most concerned with obtaining, it serves as the main conduit to the other classes. Using the example above, to get all the Download instances of a certain DataTheme the code would look something like: `Download.all.select { |dl| dl.type.theme.name == "Large scale data" }`. While it is slightly longer than calling data_theme.downloads, it is way easier to manage and maintain the relationships using the simplified structure.

