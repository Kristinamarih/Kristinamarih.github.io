---
layout: post
title:      "Sinatra Project"
date:       2019-09-24 00:37:35 +0000
permalink:  sinatra_project
---

### Save Me A Plate

For this project, I decided to do something related to food waste - I wanted to create something that would help connect a restaurant's leftover food with interested customers. I wanted to build something that would allow restaurants to sign up and post their remaining food each day for people to browse and claim. I studied environmental studies in college, and thought this would be a fun way to incorporate that into my coding! To quote the homepage of my app:

> One third of the food produced in the world for human consumption every year
> — approximately 1.3 billion tonnes — gets lost or wasted. Food losses amount to roughly
> $680 billion in industrialized countries and $310 billion in developing countries.

To begin, I made a list of all the things I wanted my MVC app to be able to do, following CRUD (create, read, update, delete). I determined I'd need a Meal and a User model, because I wanted restaurants to have full CRUD functionality to create, update and delete meals, but only wanted users to be able create accounts and view available meals. Once I had an idea of my models, database, and controllers, I used the Corneal gem to create the scaffolding for my Sinatra app.

I struggled a little bit with creating the helper methods and building the functionaility required to identify two different kinds of users with differing access to the app, but really enjoyed the learning process and seeing how everything came together bit by bit. I figured this out by creating a boolean in the User table for Restaurant, and a ``def is_restaurant?`` helper method which I used along with my other helper methods throughout my controller to control access. 

This was a challenging project for me, but I had a lot of fun trying to do something totally new and adding functionality that I hadn't encountered in labs before. I hope to return to this project in the future to refactor my code and add some useful features! 
