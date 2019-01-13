---
layout: post
title:      "Sinatra CRUD Application"
date:       2019-01-13 23:02:36 +0000
permalink:  sinatra_crud_application
---


For this Sinatra project, I decided to make a *CRUD* (Create, Read, Update, Delete) application with a bit of added functionality. The function of the application is to act as an advanced 'Website Bookmark' tool. It allows you to add a website, followed by attaching a tag to the website so that you can quickly filter your websites out. The tag may be: work, food, family, shopping, blogs, etc.

You begin by creating a profile. This process requires you to verify your password and contains salted password hashing by way of the `bcryp` ruby gem. 

From a broad view, the app contains three separate tables: 

1. Users - username, email, password <br>
**User `has_many` websites, and `has_many` tags `through` websites**
2. Tags - content <br>
**Tag `has_many` websites**
3. Websites - content, user_id, tag_id <br>
**Website `belongs_to` user, and `belongs_to` tag**


There were a variety of unforseen challenges with this website. First, when a User creates a website, I need to make sure that I run various checks on the user input - it's not always the case that the user will use `https://` (more than likely, they won't). It also turns out, that if a user inputs `www.`, it will be interpreted as a GET request. This means that I had to add `https://` if a user inputed a website like `youtube.com` and if a user inputed `www.youtube.com`, I need to substitute `www.` with `https://`. 

The next challenge I faced when developing this application was the discovery that a user might not remember all the tags that they have created. If a user created a tag `blogs`, they may not want to create another website with the tag of `blogging`. This told me that I should probably add some type of autocomplete/dropdown functionality that was populated from that specific users `Tags` table. This was a true test of my database associations. I needed to make sure that one User isn't seeing their autocomplete populated with a different User's tags. 

In the future, I would like to add a way for a user to add multiple tags to a website, and to set their website to 'private' or 'public'. This way, if someone wanted to find websites that match certain tags, they could search public tags. There could also be a 'suggested' sites functionality. Google is a great way to find a site that you want, but it doesn't build a profile and suggest cites to a user based on their currently bookmarked items.






