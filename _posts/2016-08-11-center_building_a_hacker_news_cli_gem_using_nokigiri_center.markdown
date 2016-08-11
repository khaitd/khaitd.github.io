---
layout: post
title:  "<center> Building a Hacker News CLI GEM using Nokigiri </center>"
date:   2016-08-11 15:53:18 +0000
---


  <center> ![](https://s3.amazonaws.com/GoRoost-Heroku/wp-content/uploads/2014/08/hacker-news.jpg) </center>
	
The first part of building this CLI consisted of determining which functionality would be most relavent to the end user. Since I'm scraping Hacker News, this phase was straight-forward. Displaying the names of the articles was clearly the information that users would need the most, followed by a few other descriptors such as the upvote count, source, comments, time posted, as well as the posters username. I decided to display, what I considered the most relavent information in the following format. 

![](http://i.imgur.com/hwpQqsr.png)
The colorize gem was useful for making the article title, source, and score attributes distinct, allowing me to avoid using a table. I also added a simple menu to provide a user command interface.

The heart of my program was the CLI and News classes. A new instance of the CLI class is called immediately when the program starts up, and it calls a "call" instance method which is also created in the CLI. The call method invokes two other methods, "list_news" and "menu". These methods create instances of the News class and utilize its instance methods to scrape [Hacker News](https://news.ycombinator.com/).

![](http://i.imgur.com/Ji32d1i.png)

The scrapping section of the News class was pretty straight-forward due to the simplicity of the HTML formatting written by the Hacker News Web Dev team. I optimized my class to recieve mass data assignment upon initialization, and I used an each loop to parse over the Nokogiri object, collect the respective data into a hash, and initialize a "News" object with the retreived data. I added two more loops to scrape the upvote count and the comment id (which I use to access an articles comment section) It would be useful to allow users to access the comments section of a specific article. Upon entering a specific article I scraped one layer deep in it to retreive it's id number. Appending this id number to the hacker news URL gets the full pathname to access the article. 

To open the article in a browser I used the handy [Launchy](https://rubygems.org/gems/launchy/versions/2.4.3) Gem. It accepts a URL and launches it in your default browser of choice.


I decided to challenge myself, and add a useful layer of functionality to my CLI app by creating a sort method that would reorder the articles according to their up vote count (without using rubys built in .sort method). My first iteration of this sort method used two while loops which ran in exponential time(O(n^2)). I am currently refactoring my code to use the merge sort algorithm to increase performance. 

![](http://i.imgur.com/a1Pemwi.png)
A sorted list of hacker news articles.


I finally added it all together in the CLI class, when called, it prints a menu of possible commands and prompts the user to input a command and voila we have a functioning Hacker News CLI app using the Nokogiri scraper.    








