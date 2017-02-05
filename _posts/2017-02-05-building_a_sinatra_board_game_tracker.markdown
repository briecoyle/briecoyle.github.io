---
layout: post
title:  "Building a Sinatra Board Game Tracker"
date:   2017-02-05 16:46:15 -0500
---


So, here I am. I've reached a second major milestone in the Learn curriculum. I can't believe how much I learned during the CLI gem application project. While that first project cost me about a month of trying, I was able to conceptualize and execute this application in about a weekend. I approached this second project with an entirely different mindset, which focused on the stepwise execution of each basic feature from the ground up instead of trying to implement everything and the kitchen sink from the start.

This project is a basic Sinatra-based CRUD application that allows users to create and maintain an inventory of their board games. New board games can be added by users with the attributes for a name, description, and appropriate number of players. Additionally, one can add an existing board game to their collection, which with creating a running account of all of the users who own the same games.

## Creating a File Skeleton
I started out this project by creating a repository on Github and cloning the repo into Atom. As such, the original directory for the project was strikingly bare bones. I started by adding all of the files I would need to set up a Sinatra project with ActiveRecord data permanence. A Rakefile, Gemfile, README, and config.ru were added to the file tree. At this point, I didn't want to add any content to these files. This was where I learned my first lesson from the previous project. It was tough (honestly!) not to want to fill up all of the files with instructions I was writing in my head, but I forced myself not to. I added a directory for my application with separate directories for models, views and controllers, as well as an environment in the config directory. Suddenly, an application was born. Well...

## Adding the First Few Lines
I used previous projects to help guide the contents of my Gemfile. I knew that I needed to rely on several gems for this project including the biggies: sinatra, activerecord, sinatra-activerecord, and rake. I also knew that I needed sqlite3 to support activerecord, thin to host my application on a web server, bcrypt for password incryption, and rack-flash3 for flash messages to used. I also included some development gems for my own benefit: shotgun, pry, and tux. At this point, I also edited the README and included the CONTRIBUTING and LICENSE terminology from the Contributor Covenant and MIT's open source page respectively. I fleshed out the Rakefile, config/environment and config.ru to tie all of these pieces together. After running bundle install, I was ready to get down to business.

## Setting Up the Database
Almost. I would have to find some way to manipulate the data I was creating to transfom my "playing in the sandbox" into a more productive venture. I used rake to make tables in my database for both users and board games, and I decided to create a join table to facilitate a has-many to has-many relationship. After the databases were made, I created models for these which inherited from ActiveRecord::Base and used validations to ensure their attributes. I also eventually added a seed file with a few users and a few board games that I could use to play around with in the browser. I ran my migrations through rake and turned my attention to my controllers.

## Making Something that Looks Like Something!
I had finally reached a point where I could start to write code that would "actually show up" on a web page. I recognized that all of my hardwork to just set up my basic framework had paid off when I decided to write:

```
get '/' do
"Hello World"
end
 ```

in my Application Controller. I ran shotgun from my terminal, made my way to the IP address provided and there it was. Plain as day. Hello World plasted across my screen. It's hard to quantify that feeling. Maybe I'll dedicate another post to the revelations of actually finding my passion in life. Let's stick to the technicalities here, shall we?

At this point, I was maybe sadly truly proud of myself for just confirming that my browser would respond to this most basic request instead of linking to a new view right away. It's a good thing I did because when I added an index page to the view directory and linked to it in the get '/' request, and ran shotgun... nada. It took a solid half-hour to realize that I had never specified this message as HTML in the view.erb file. But eventually, I realized my mistake, patted myself on the back for general stick-with-it-ness and started to add the fun stuff.

##### To Be Continued.
