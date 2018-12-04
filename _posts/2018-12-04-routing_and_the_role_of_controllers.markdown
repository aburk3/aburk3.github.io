---
layout: post
title:      "Routing and the Role of Controllers"
date:       2018-12-04 14:52:59 +0000
permalink:  routing_and_the_role_of_controllers
---


Now that I have finally made it to Sinatra, I'm getting a much more wholistic picture of what an application is like under a MVC framework. Prior to this point I have been dealing exclusively with the the back-end - whether that be ruby, ActiveRecord, or sqlite3 - or with the front-end (JavaScript, HTML, CSS). There hasn't really been an indication of how this would all be integrated and how everything would communitcate/pass data.

Enter Controllers. My impression of Controllers are that they are the traffic signalers of the MVC framework - nothing really knows where to go without the Controller. Have a data from a form that needs to be passed to the Model so you can do some Ruby on it? You don't shout "MODEL!" and hear the Model shout back "HERE!" 

Instead, you allocate that duty to the Controller. You tell the Controller where the Model is, and you tell the View where the Controller is. The Controller therefore is able to mediate the interaction between the two in an efficient, well-coordinated manner.

I'm only at the beginning of interacting with the MVC framework so I can't wait to see what else is to come!


