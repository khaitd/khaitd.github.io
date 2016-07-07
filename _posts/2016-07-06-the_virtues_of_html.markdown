---
layout: post
title:  "The Virtues of HTML"
date:   2016-07-06 19:37:47 -0400
---


![](http://i.imgur.com/Cqw6vh2.jpg)

Its not an understatement to claim that HTML is a simple programming language to learn. This fact initially lead me to underestimate just how important HTML was for the viability of the web. Upon closer inspection I’ve grown a deeper respect for the markup language for its unparalleled dominance of the web, and a deep appreciation for the brilliance of visionaries like Vannevar Bush, and Tim Berners-Lee. 

![](http://specs.adfox.ru/help/images/swiffiFlashHTML.png)
HTML provides instructions on how to display content, and explicitly states how different sections on a website are suppose to work together.

HTML, CSS, and Javascript form the foundation of mostly all web sites, and HTML is unequivocally the most fundamental of the three. Simply stated if we did not have HTML we would not have the internet. 


![](http://upload.wikimedia.org/wikipedia/commons/e/ea/Vannevar_Bush_portrait.jpg)

In 1945 Vannevar Bush, an American engineer, and inventor who headed the U.S. Office of Scientific Research and Development published an essay in which he foresaw a futuristic proto-hypertext device that could be used to compress and save all types of information such as books, records, and communications, that would be "mechanized so that it may be consulted with exceeding speed and flexibility.” It was called the memex and its purpose was to supplement human memory. A Memex would hypothetically store - and record - content on reels of microfilm, using electric photocells to read coded symbols recorded next to individual microfilm frames while the reels spun at high speed, stopping on command. The coded symbols would enable the Memex to index, search, and link content to create and follow associative trails. Bush’s vision sparked the development of hypertext technology, eventually leading to the World Wide Web. 

   ![](http://s-media-cache-ak0.pinimg.com/236x/22/34/64/2234641341ab69b987183f611d16935d.jpg)

	
HOW IT WORKS / TECHNICAL / Web Browsers

HTML documents are interpreted by web browsers which currently conform(for the most part) to specifications in order to avoid compatibility issues. The browser has a rendering engine that parses HTML and CSS, and displays the parsed content on the screen. Tests such as [acidtest](http://acid3.acidtests.org) show how well a browser renders a page and most score highly. 


The way the browser interprets and displays HTML files is specified in the HTML and CSS specifications. These specifications are maintained by the W3C (World Wide Web Consortium) organization, which is the standards organization for the web. For years browsers conformed to only a part of the specifications and developed their own extensions. That caused serious compatibility issues for web authors. Today most of the browsers more or less conform to the specifications.


 For example if the requested content is HTML, the browsers rendering engine parses HTML and CSS, and displays the parsed content on the screen.
  
![](http://i.imgur.com/usAF3xQ.png)
 

A parser is a software component that takes input data (frequently text) and builds a data structure 

![](http://i.imgur.com/xZ4Eo8z.png)

The rendering engine will start parsing the HTML document and convert elements to DOM nodes in a tree called the "content tree". The engine will parse the style data, both in external CSS files and in style elements. Styling information together with visual instructions in the HTML will be used to create another tree: the render tree.

The render tree contains rectangles with visual attributes like color and dimensions. The rectangles are in the right order to be displayed on the screen.

After the construction of the render tree it goes through a "layout" process. This means giving each node the exact coordinates where it should appear on the screen. The next stage is painting–the render tree will be traversed and each node will be painted using the UI backend layer.




It's important to understand that this is a gradual process. For better user experience, the rendering engine will try to display contents on the screen as soon as possible. It will not wait until all HTML is parsed before starting to build and layout the render tree. Parts of the content will be parsed and displayed, while the process continues with the rest of the contents that keeps coming from the network.


Sources and further readig:
[html5rocks](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
[Wiki SGML](https://en.wikipedia.org/wiki/Standard_Generalized_Markup_Language)
[Wiki HTML](https://en.wikipedia.org/wiki/HTML)
http://www.tech-faq.com/how-does-html-work.html
https://www.smashingmagazine.com/2010/09/html5-the-facts-and-the-myths



