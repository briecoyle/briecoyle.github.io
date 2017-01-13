---
layout: post
title:  "My First Ruby Gem"
date:   2017-01-13 02:17:02 +0000
---

This is not a blog post about how easy it is to build a ruby CLI gem; this is a blog post about how hard it is to build a ruby CLI gem.
## Early visions
When I first started this project, I joined a Study Group to brainstorm ideas. Right off the bat, the moderator from Learn warned me that my website might be a little challenging to scrape. I had decided that I wanted to create a list of the upcoming television premieres based on [this webpage](http://www.metacritic.com/feature/tv-premiere-dates). Each show is conveniently packaged as a row in a table. However, the biggest challenge I ran into was that the dates for each list of premieres was also a row in that same table; this established the premiere date as a sibling of each show rather than a parent. There are plenty of HTML classes that allow for easy scraping of the information for data, but I ran into a lot of trouble when trying to define the association between the dates and the shows. After logging off of the chat, I was inspired and started to brainstorm the overall layout of my CLI app. Here's what I felt I needed.

1. lib/Scraper class - load and scrape the webpage, identify the css selectors for all of the information
2. lib/Premiere class - (has many Shows) date
3. lib/Show class - (belongs to a Premiere) title, genre, network, time
4. lib/CLI class - define the user interactibility of the app
5. bin/run.rb - initial call to launch the app

## Where I went wrong
I started with the "hardest part" of the project. I immediately created the Scraper class, and used nokogiri and open-uri to get the HTML from the Metacritic website. I started playing with (and finally understanding?) pry and the development tools in Chrome to target information on the page. Turns out the scraping part wasn't that hard!

In the initial iteration of my Scraper class, I incorporated the CSS selectors into methods of the Scraper class and create hashes and arrays for each show and premiere. As I moved into the Premiere and Show classes, I found myself undoing much of the work of the Scraper class during my custom initializations of these objects. Eventually, I realized that I had muddled up the purpose of the classes, and I really needed to use the Scraper to just gather the HTML of the page, and then use each Object to take the raw HTML and parse for the relevant piece of information.

At this point, I created a new branch for my project and started to trim down all of the extraneous code. I moved the parsing to the Show and Premiere classes and streamlined the Scraper methods. Then I started to run into trouble again.

Because the premiere dates are listed alongside the shows on the Metacritic site, I was having a difficult time connecting the information between these two classes. There was never a set number of shows per premiere date. The premiere date was not a parent of each collection of classes. I tried scraping both the date and the shows that followed that date, but it seemed to just collect a list of all of the shows that follow any date. I looked for a selector that would allow me to select the previous sibling of the first show, but I was only able to find a reference for a following sibling. At this point, I was frustrated. I felt that I reached a stopping block, and so I tried to shift gears towards building the CLI. However, my brain was pulled in so many directions, that I found myself changing too many files at once and causing things to break. And break. And break.

## Necessary inspiration
I decided to put my work aside at this point and rewatch the video walkthrough of the CLI Gem Daily Deal. Pretty much instantly, I realized that I started this project totally backwards. Avi recommends that you start with the CLI. Building it without worrying about any of the scrapers or objects that would eventually be necessary. I was the living embodiment of *facepalm* when I realized how much sense this made. Of course! If I could start with the larger infrastructure, I wouldn't run into the same problems I had in the previous iteration of my project. I was also inspired to ensure that my app would be available as a gem for the extra bonus points. 

## Starting over, again
At long last, I began my project one last time. This time, I created a whole new git repository and initiated the necessary files using bundler gem. I started with the CLI class (finally) and stubbed in the necessary representative data as I went along. When I had created a servicable interface, I moved on to the Objects that would make the CLI have meaning. Again, I was overzealous in my nature and created separate classes for each attribute I wanted my show listing to have. As such I created separate classes, and files, for the Genre and Network for the show. I imagined that both the Genre and Network would have many instances of Shows, and a Show would belong to a Network and a Genre. I then created the Scraper class and included all of the hard work I had accomplished days prior.

Unfortunately, I hit one last block when I added the requires to the single ruby file outside of the lib directory. Through testing with pry, each Class file was distinct from the others and I could not have them communicate with one another. I believe I was unable to find the correct order of the require_relatives for my Class files. After sleeping on the issue, I came to an simple solution. I could make create class variables to hold the list of genres and networks that belonged to all shows. FINALLY, I had a working program that truly did what I was hoping it would...

<iframe width="560" height="315" src="https://www.youtube.com/embed/BJW4LrbokH8" frameborder="0" allowfullscreen></iframe>

...apart from that whole collecting the date issue. That was never able to be resolved. Which brings me to!

## Future directions
* premiere dates for each show
* collecting only the next two weeks of shows
* add another website to scrape for show descriptions
* distinguish networks as either streaming or broadcast
* create a fully functioning published gem
