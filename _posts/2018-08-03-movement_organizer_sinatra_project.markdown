---
layout: post
title:      "Movement Organizer Sinatra project"
date:       2018-08-03 20:01:57 +0000
permalink:  movement_organizer_sinatra_project
---


Just finished my Sinatra project, it was a lot of fun. I decided to base my project on business ideas that have crossed my mind related to my martial arts and fitness practice. Sometimes I wish that I could have a way to easily collect workouts for my clients with details about the movements. That way my client can understand what I am wanting them to perform without having to send lengthy emails about exercise instructions, videos and pictures. Thus Monks And Ninjas fitness site was born. Pulling together other ideas I made the site so that guests will see upcoming events, about us, teachers, and contact. If guest decides to signup, they will have access to our users section which includes connecting to our network of users, newsfeed, movement organizer and posts. User will be able to create, destroy, read, and edit movements/posts, as well as edit their account info. Sinatra and ActiveRecord are used to create the dynamic site. 

In the beginning of the project, much of my knowledge of Sinatra was still quite muddled. I really wanted to tighten my skills and experiment with many of the details leading up to the project that I felt I may have rushed through. This included such things as CSS, adding images, seeds.rb, migrations, multiple controllers and models with various model relationships, detailed overview of Rack (which you can read in my previous post [here](http://http://josephjimenez.info/daydreaming_of_rack)), and lastly join tables. 

Some problems I came across was organizing all the files in their proper folders. Examples include:

* Making sure my logo was in the public folder, otherwise I could not access the pic. 
* Are my important or often used methods either in my Helpers folder or in my Concerns folder. Making the right choices would simplify my html or controllers. 
* Using migrations to add columns as opposed to just adding it to the original migration.
* Linking to a css file from the layout.erb was not possible, I imagine it has something to do with being an .erb file not .html. I ended up just putting the css directly in the layout and tried my best to keep it short. 

In conclusion the project was not difficult in the sense of writing code but in keeping track of all the moving parts, a much higher degree than the previous cli project. Refactoring and taking advantage of all the tools such as pry, shotgun, and tux were exceptionally helpful in understanding the flow of information and not get overwhelmed.  I imagine the Rails project will be even more complex. I did notice some patterns in the code and files that I imagine Rails will be able to streamline as I did find myself copying and pasting a bit. Lastly I made sure to have my wife play with the application in hopes of breaking it. This proved to be helpful, especially when I started to feel too comfortable with the project.
