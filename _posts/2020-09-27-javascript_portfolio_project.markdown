---
layout: post
title:      "JavaScript Portfolio Project"
date:       2020-09-28 01:19:45 +0000
permalink:  javascript_portfolio_project
---

## In A Flash

For my JavaScript portfolio project, I was tasked with creating a Single Page Application using a Rails API backend and JS on the frontend. I needed to use asychronous code to handle interaction between the client and server sides, and make at least 3 AJAX calls with fetch requests covering at least 2 CRUD actions. I decided to make a simple flashcard app! This project is built with JS, HTML, and Bootswatch for styling on the frontend. Starting this project was a bit overwhelming for me at first - I struggled to understand the flow of things while working through the JS labs, and didn't start connecting the dots of event listening, manipulating the DOM, communication with the server etc until I was well into my project. 

### The backend

My first step was to set up my backend. I created the Decks and Cards controllers, and set it up so that a deck has many cards, and cards belong to a deck. Below is what my schema looks like:

```
create_table "cards", force: :cascade do |t|
    t.string "term"
    t.string "description"
    t.bigint "deck_id", null: false
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
    t.index ["deck_id"], name: "index_cards_on_deck_id"
  end

  create_table "decks", force: :cascade do |t|
    t.string "name"
    t.string "category"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end
```

It definitely took a little while to refresh my Rails memory after being in JS-land for so long! After building out the controller methods and setting up the models and serializers with the fast JSON AP gem, I moved on to the frontend.

### The frontend

Since I began, I've refactored the majority of my code multiple times, and also had to take an unexpected months long break from my project. Revisting my code after my break was interesting - I was stressed about how disorganised and messy my initial code now looked, and I think the major refactoring process that followed was really helpful, and resulted in an increased comfort with JS.

My initial page shows a form for creating a new Deck, and a table of previously created decks below. Users can click on a deck, which opens a modal displaying a form to create new cards for that deck, and also allows users to click through each individual card for the deck.

I created OOJS classes for Decks and Cards, and put the rest of my JS code in my index.js file. The OOJS classes contain constructors, static functions, and rendering functions to display the deck and card detailson the DOM. The index.js file is responsible for pretty much everything else, such as the event listening/handling, AJAX calls, manipulating the DOM and so on.

I dealt with several new things during this project, one them being modals. I really wanted to incoporate some styling in this project, and went into it with a pretty clear idea of what I wanted the user experience to be. It was definitely a struggle/learning process to make some of those concepts a reality! There are a lot of features I'm excited to build out in the future, such as a way to toggle between study and play mode for the decks, and to incorporate my Users model. I'd also love to have stats for how well users perform "playing"their decks.
