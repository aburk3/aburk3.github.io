---
layout: post
title:      "Habit Tracker React Redux Project"
date:       2019-07-29 13:19:53 +0000
permalink:  habit_tracker_react_redux_project
---


Having spent a fair amount of time on my [Rails project](https://pickleballsocial.herokuapp.com/) , I decided to simplify this React/Redux project. I decided to make a simple habit-tracker application to demonstrate how React application, utilizing Redux for state management, can utilize a Rails API backend. 

I started this project by creating the Rails API, the database (using postgreSQL), the routes, and finally the controllers. To ensure that there were no cors problems when making requests from the client side, I added the `rack-cors` gem to my bundle. Next, I built out the react app structure with the `create-react-app` generator.

I implemented Thunk as middleware to use in conjunction with React/Redux and add functions inside the action creators. This means that I was able update the Redux store with data that was returned from the Rails API. 

> If only there were some way to teach Redux how to deal with functions as actions…
> 
> Well, this is exactly what redux-thunk does: it is a middleware that looks at every action that passes through the system, and if it’s a function, it calls that function. That’s all it does. - [Dave Ceddia](https://daveceddia.com/what-is-a-thunk/)

Putting everything together, my habit tracker application allows for a user to go to a form page where a new habit can be created with a name and description - this creation process makes a post request to the Rails API, which creates and save an instance of the `habit` in the database. A user can then utilize the increment/decrement functionality to keep track of how often the habit was executed. View the GitHub repo [here](https://github.com/aburk3/habit-tracker)!
