---
layout: post
title:  " Building a Hacker News CLI GEM using Nokigiri "
date:   2016-08-11 11:53:18 -0400
---


   ![](https://s3.amazonaws.com/GoRoost-Heroku/wp-content/uploads/2014/08/hacker-news.jpg) 
	
The first part of building this CLI consisted of determining which functionality would be most relavent to the end user. Since I'm scraping Hacker News, this phase was straight-forward. Displaying the names of the articles was clearly the information that users would need the most, followed by a few other descriptors such as the upvote count, source, comments, time posted, as well as the posters username. I decided to display, what I considered the most relavent information in the following format. 

![](http://i.imgur.com/hwpQqsr.png)
The colorize gem was useful for making the article title, source, and score attributes distinct, allowing me to avoid using a table. I also added a simple menu to provide a user command interface.

The heart of my program was the CLI and News classes. A new instance of the CLI class is called immediately when the program starts up, and it calls a "call" instance method which is also created in the CLI. The call method invokes two other methods, "list_news" and "menu". These methods create instances of the News class and utilize its instance methods to scrape [Hacker News](https://news.ycombinator.com/).


```
class HackerNews::CLI

  def call
   list_news
   menu
  end

  def list_news
     puts "Today's Hacker News:"
     @news = HackerNews::News.today
     @news.each.with_index(1) do |article, i|
       if i < 10
         print " #{i}. #{article.title} - "
       else
         print "#{i}. #{article.title} - "
       end

         print "SOURCE: #{article.source}".colorize(:blue).chomp
         puts  "- SCORE: #{article.rating}".colorize(:red)
     end
  end

  def menu
    puts "------------------MENU ITEMS----------------------"
    puts "1 - ENTER the number of the article that you want to link to. [1 - 30]"
    puts "2 - Enter S to SORT the LIST"
    puts "3 - Enter C access an articles comments"
    puts "4 - Enter E to to exit"
    puts "--------------------------------------------------"
        input = gets.chomp.downcase
        if input == 's'
          sort_news
          menu
        end
        if input == 'c'
           puts "Which article's comments do you want to access? [1 - 30]"
           input_comment = gets.chomp
           link_comments(input_comment)
           menu
        end
        if input.to_i > 0 && input.to_i <= 30
           link_news(input)
            menu
        end
        if input == "e"
          exit
        end
  end
	
```

The scrapping section of the News class was pretty straight-forward due to the simplicity of the HTML formatting written by the Hacker News Web Dev team. I optimized my class to recieve mass data assignment upon initialization, and I used an each loop to parse over the Nokogiri object, collect the respective data into a hash, and initialize a "News" object with the retreived data. I added two more loops to scrape the upvote count and the comment id (which I use to access an articles comment section) It would be useful to allow users to access the comments section of a specific article. Upon entering a specific article I scraped one layer deep in it to retreive it's id number. Appending this id number to the hacker news URL gets the full pathname to access the article. 

To open the article in a browser I used the handy [Launchy](https://rubygems.org/gems/launchy/versions/2.4.3) Gem. It accepts a URL and launches it in your default browser of choice.


I decided to challenge myself, and add a useful layer of functionality to my CLI app by creating a sort method that would reorder the articles according to their up vote count (without using rubys built in .sort method). My first iteration of this sort method used two while loops which ran in exponential time(O(n^2)). I am currently refactoring my code to use the merge sort algorithm to increase performance. 

![](http://i.imgur.com/a1Pemwi.png)
A sorted list of hacker news articles.


I finally added it all together in the CLI class, when called, it prints a menu of possible commands and prompts the user to input a command and voila we have a functioning Hacker News CLI app using the Nokogiri scraper.    








