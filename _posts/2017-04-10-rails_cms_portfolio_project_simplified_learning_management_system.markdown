---
layout: post
title:  "Rails CMS Portfolio Project: Task Manager"
date:   2017-04-10 11:40:46 -0400
---


A color-coded task manager that allows users to delegate tasks to others.

### *1) Brainstorming the Rails Portfolio Project*

* Completion of the Learn Curriculum
* Productive (?) procrastination
* $100 and a valid email address
* Deep seeded frustration in the tools associated with one's current occupation

When you first reach the Rails Portfolio Project, you will notice that you have a half dozen unwatched lectures in the Learn curriculum. Before starting to write any code, but after reading the requirements at least twice, procrastinate by watching lectures about object orientation, authentication, and authorization. Spend $100 on Rails tutorials and literature. Sign up for 3 email courses about blogging. Reread the portfolio project requirements. Decide to incorporate model testing in your project and code-along with setting up a rails project that utilizes rspec testing. Oops, you've begun. Title your code-along project Classroom Manager because you accidentally ended up as a highschool biology teacher at your alma mater. 

### *2) Initializing a Git repository*

* Terminal
* [Rails: Testing Our Models](http://instruction.learn.co/video_lectures/101)
* Atom text editor

>###### A note from the cook:
>*But wait, I thought you titled your project Task Manager, not Classroom Manager? Well, I initially started by project with the intention of fully immersing myself into test-driven development. As a scientist/teacher/armchair-psychoanalyst, I pride myself on my critical eye. Since science is all about asking questions, I often catch myself in "Now, what does this data really show? Can I believe that? Can you make that claim? What do we know?" I think the constant questioning of "What do we know?" is essential in web development, and the TDD mentality of intentionally setting expectations about the program before execution felt a lot like the process of experimental design. As such, I fell down a bit of a rabbit hole during the process and unfortunately lost my path on the way there. I learned a lot about TDD and started a code-along with one of the Learn lectures, but I found myself veering away from the requirements of the project. And, so Task Manager was born. Perhaps one day, Task Manager will morph into Classroom Manager anyway.*

Is there anything better than the fresh bite of a new Git file? This one little repo has the possibility to be anything, to solve any problem. Popping open Terminal and typing `rails new ...` is oh so exhilarating. Be sure to savor the moment of `git init` and cherish the satisfaction of your first `git push`. It's possible at this stage that you might have forgotten that you need to set your origin to a new GitHub repository for ultimate code mobility, but never fear! Anyone can ~~cook~~ code!

### *3) Embracing the Rails MVC*

* List model: name; has many tasks
* Task model: name, due_date, status; belong to a list

The Model-View-Controller system can certainly be a helper or a hindrance at this stage. I have found that the best strategy is one of utter mindfulness. Being present and attentive to how Rails is communicating saved me a lot of heartbreak while I was learning how to code in Rails. Try to set up the first model that does not have any necessary associations. For me, that was the List model. Associate the model with your database and include some parameters that you are interested in. Then, create a controller that will communicate between the database, create a model based on saved information, and relay that information to the view. The view will then use that formation to display it to the user on the front end of your application. Reiterate this process for as many models as you may need. At each step of the process, you should be able to read feedback from Rails as it requests your next task. Voila! You are well on your way to your own Rails application!

### *4) Adding and authenticating users*

* Shared_list model: user_id, list_id, permission; joins user to a list
* User model: devise parameters, omniauth parameters, first_name, last_name, image; has many shared_lists
* Devise
* Omniauth, omniauth-oauth2, and omniauth-google-oauth2

At this point, you would probably like to add users to this application. The first step is to create a User model itself. Unfortunately, the first first step of this would be to install the Devise gem for your particular application (which I suppose makes adding Devise to your Gemfile and running bundle install the first first first step). Devise is a framework built on Rails to standardize user signing up, signing in, and logging out. It is magical, but built on real-life concepts and manipulatable ruby files. In addition to other modules, you want to ensure that your model is omniauthable by adding a uid and provider as strings to your database migrations. Straight from the box, Devise only allows for users to sign up/in with an email and password, if you would like to add additional information or alternative sign-ins, you will need to do some tweaking. [This](http://jacopretorius.net/2014/03/adding-custom-fields-to-your-devise-user-model-in-rails-4.html) is a very good guide on how to do this. Omniauth is pretty self-explanatory through their README, but you may be a little frustrated with Google's end of this authentication, as it can take a few hours for your registered credential URIs to be saved.

### *5) Authorizing users*

* Pundit

Finally! The last stages of your brilliant masterpiece. I can smell the faint wafts of success already! But, there is one crucial, tedious, and occasionally mind-bending step to this process - authorization. While we ensured that users are who they say they are in during the previous step, we still need to regulate what they are allowed to do. In many cases, you will set up different permissions, or policies in Pundit-speak, based on a user's role in the application. Naturally, an administrator should be able to do more than a guest should. However, you may run into more complicated permissions, as is the case in this particular project. User permissions are based on the user's ownership of a specific list. If they created the list, they own it and can do whatever they would like to it. However, if the list is shared with them by another user, as a colloaborator, they can only update the status of different tasks and add tasks to the list, but they cannot delete a task or rename a list. Finally, if they have no association with the list, they shouldn't even be able to see it. After several sleepless nights of wrestling with this issue, I found that the majority of this problem was solved through the use of Pundit's scopes, and setting permissions based on the shared_list permission of a specific instance of a list, after filtering out the lists that weren't associated with the user.


