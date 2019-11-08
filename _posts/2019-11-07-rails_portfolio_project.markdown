---
layout: post
title:      "Rails Portfolio Project"
date:       2019-11-07 19:31:14 -0500
permalink:  rails_portfolio_project
---


## PlantFriend

For my Rails Portfolio Project, I wanted to build something that, in its fully developed stage, could be useful in my community. I often seen people posting about fruits and veggies for sale that they've grown in their gardens on social media, and decided to make a little online farmer's market of sorts. The initial mapping out of object relationships was a challenge for me - I knew exactly what I wanted my app to do and look like, but it was tough to commit to a direction.

So for basic functionality, I wanted users to be able to:

1. Sign up/log in with Google
2. Create, edit or delete products
3. View other people's products
4. Comment on products
5. Send direct messages to other users about their products
6. Log out

I accomplished (most) of these with the following object relationships:

User:

`has_many :products, dependent: :destroy`
`has_many :comments, dependent: :destroy`
`has_many :commented_products, through: :comments, source: :product`
`has_many :conversations, :foreign_key => :sender_id`
		
Product:

`belongs_to :user`
`belongs_to :category`
`has_many :comments, dependent: :destroy`
`has_many :users, through: :comments`

Comment: 

`belongs_to :user`
`belongs_to :product`

Category:

`has_many :products, dependent: :destroy`

Message:

`belongs_to :conversation`
`belongs_to :user`

Conversation:

`belongs_to :sender, :foreign_key => :sender_id, class_name: 'User'`
`belongs_to :recipient, :foreign_key => :recipient_id, class_name: 'User'`
`has_many :messages, dependent: :destroy`

Phew! It was lot of work. I wanted to challenge myself by creating direct messaging functionality, and was able to get all aspects of this working except for one...the ability to start a new conversation with a user. By cheating (through url manipulation), I've tested out my messaging and it works - I'm able to send messages back and forth between users complete with timestamps. After much research and quite a few study sessions, I don't believe the messaging I'm trying to create can be done the way I want with Ruby on Rails alone, and am excited to return to this code after JavaScript!

This project was beautifully frusterating and fun for me to work on, and it's exciting looking back on my Sinatra project to see how far I've come. I've left this project with an even longer list of features I want to build out and other Rails projects I'd love to work on (if I can find the time). I've found that Rails is as magical as everyone says, but requires a lot of patience, determination and coffee to work out :') Still have a very long way to go, but excited for the journey!






