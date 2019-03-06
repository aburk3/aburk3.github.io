---
layout: post
title:      "Rails Project - MyClub"
date:       2019-03-06 12:21:02 +0000
permalink:  rails_project_-_myclub
---


It feels like this Rails section has completely flown by, but I've learned so much along the way. The initial transition from Sinatra to Rails was difficult to come to grips with, but like almost everything since I began programming, it has gotten easier over time.

For my Rails portfolio project I decided to make a simply application called [MyClub](https://github.com/aburk3/MyClub). This web application allows a User to create a profile, create a Club with a title and description, followed by creating meetings that are associated with that club. I created four tables for this application:

1. A `users` table
2. A `clubs` table
3. A `meetings` table
4. A `user_clubs` table

The `user_clubs` table in this case acts as the [join table](https://guides.rubyonrails.org/association_basics.html). A `user` has many `user_clubs` and has many `clubs` through `user_clubs`. A `club` has many `user_clubs` and has many `users` through `user_clubs`. A club also has many `meetings`. This means that there is a two-way relationship between User's and Clubs. It also means that a meeting cannot exist outside of a Club. 

I felt like this is a good idea for an application, not so much for the use cases, but rather the learning opportunity. My intuition is that this type of applicaiton is a low level view of many CRUD applications (Facebook, Twitter, Instagram, etc.). It allows for a User to be created. It allows a User to join OR create a club. It allows a User to create 'meetings' from within a club. At base, many of these features are small deviations from the base framework of the applications we know and love - so I wanted to familiarize myself with them. 

I would say that the most difficult part of this project was configuring the nested form to create Meetings within Clubs. There is so much going on behind the scenes with Rails Forms that it can be easy to forget what tools are really available to you. I've found that often times that the answers to the hardest problems was to simply appeal to the documentation - which I've generally stayed far away from in the past.

One of the more excited parts about this lab was working with [omniauth](https://github.com/omniauth/omniauth). Allowing a user to login via Facebook makes the user login flow so much more fluid. The fact that the User's profile photo can be obtained as well is a bonus. One difficulty that I did encounter was with the database I had set up, which has `first_name` and `last_name` as two different columns. Facebook passes the requested information in a hash like this: 

```
oauth_name = request.env["omniauth.auth"]["info"]["name"]
```

Which meant that I had to dive into the hash to find all of the information I needed for the user, which took some time. After which, I needed to take the name that Facebook gave as first and last name together and split it for my database into first and last. Next, I needed to assign the user a randomer password if they logged in vai facebook - I decided to use `[SecureRandom.hex](https://api.rubyonrails.org/v3.0/classes/ActiveSupport/SecureRandom.html)`.

Although there is much desired in the MyClub application, it has taugh me a lot that I will carry with me moving forward. 


