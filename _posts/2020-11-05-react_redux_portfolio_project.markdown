---
layout: post
title:      "React/Redux Portfolio Project"
date:       2020-11-05 14:10:12 +0000
permalink:  react_redux_portfolio_project
---


## Time & Place

For my (final!) portfolio project, I was inspired by pre-covid times where I found myself driving all over LA for events, appointments, friends and so on. Traffic in LA makes it very difficult to get around, so if you have an engagement on the other side of town, you make a day out of it! I wanted to create an app that allows users to create meetups, and then share those meetups with friends. So, for example, if I had to be in Santa Monica at noon, I could create a meetup to notify friends that "hey, I'll be in Santa Monica in the afternoon if anyone wants to grab lunch!"

### Some serious stretch goals...

I was really excited about the potential for this app, especially because I could see it being very useful for my friends and I! Initially, I imagined using an external map API, such as the Google Maps API, to aid in creating the meetups - a user could enter a POI in the map, and then use it to create the event. Invited friends would also be able to view the event on the map. I also wanted to create a notification system so that users could recieve notifications when invited to meetups, or when their invitations were accepted. A chat feature between friends would have been cool too...

Instead, I focused on creating a MVP for my review, with the intention of building out all these cool features later!

### The backend

For my backend, I created User, Meetup and Friendship models.

Here's the schema:

```
ActiveRecord::Schema.define(version: 2020_10_15_194505) do

  create_table "friendships", force: :cascade do |t|
    t.integer "user_id"
    t.integer "friend_id"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

  create_table "meetups", force: :cascade do |t|
    t.datetime "time"
    t.string "place"
    t.string "description"
    t.integer "user_id"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

  create_table "users", force: :cascade do |t|
    t.string "username"
    t.string "password_digest"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end
end
```

I decided to try out something new to create my friendships feature, where friends are just other Users. To set this up, I included this code in my Friendship model:

```
belongs_to :user
    belongs_to :friend, :class_name => 'User'
```

Because I needed user authentication, I needed to go wayyyyy back and review some critical Rails stuff I had completely forgotten. This included setting up cookies and a sessions controller, so that users can sign up, log in, and log out of my app.

### The frontend

The React/Redux parts are where I both struggled the most and had the most fun. I was still feeling pretty confused and overwhelmed with Redux state management when it came time to start this project, and knew this is where I'd have to spend the majority of my time. Because this was my first attempt at a React/Redux project of this kind, I struggled with the flow of things, and figuring out what to implement and in what order. I set up the store, followed by my main containers, and then worked on building out individual components and the actions and reducers they'd interact with. Implementing a current user feature to allow for successful login and logout was very challenging, but getting it to work and seeing it in action was very rewarding!

Incorporating async actions to fetch from my server using redux-thunk was another big challenge for me, but I really enjoyed witnessing how powerful and flexible it was. 

I added some basic styling with Bootswatch, and also included a, external date/time selector package for my meetup input form, to add a calendar to select dates/times from, which I think greatly enhances the user experience. Configuring that took some time and effort, because I'd never worked with something similar in the past. 

Though my application is currently (seemingly) very simple, because it doesn't currently include friend and map functionality, it was a complicated build for me, and I'm simultaneously proud of what I was able to accomplish, and excited to refactor, improve, and add to the project once I don't have the time crunch of fast approaching program end date!

Happy coding! 
