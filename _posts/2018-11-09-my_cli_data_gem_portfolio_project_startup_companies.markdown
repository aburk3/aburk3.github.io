---
layout: post
title:      "My CLI Data Gem Portfolio Project (Startup Companies)"
date:       2018-11-09 11:32:49 -0500
permalink:  my_cli_data_gem_portfolio_project_startup_companies
---


I've just recently finished my first portfolio project which was a lot of fun. I decided to scrape a [page](https://www.startupranking.com/top) that ranks the top 100 startup companies. (GitHub [Repo](https://github.com/aburk3/top_startups))

From the beginning, my goal was to create use the CLI to allow a user to be presented with a list of the top 5 startup companies (scraped from the homepage) - followed by allowing the user to select a given company that they would like more information on.  This "more information" included the: 

* Location
* SR Score
* Latest funding amount in (USD)

The above-mentioned SR Score (more info [here](https://www.startupranking.com/how-it-works)) is obtained by scraping a second page that displays the details of the company. 


<h3>Now to the acutal code</h3>

The most time-consuming part of this project was undoubtedly scraping the pages for the correct information (name, location, rank, SR Score).

I ended up with code that looks like: `startups.location = doc.search(".ranks td .f32").children.css("img")[i].attribute("title").value`

Although it was an extremely tedious process to obtain the correct information, I learned a lot in the process. Such as using a dropping into `pry` after assigning the `Nokogiri::HTML(open(URL))` to a variable. After having done that you can simply attempt all the searches you want in the console without actually having to change your own code. 

The next challenge I came across was obtaining the URL of the details page for the company the user selects. The user isn't present with the URL in the CLI, but rather, with information scraped *from* the details page of the selected company. It was more specifically, a challenge obtaining the URL in a simple, non-hardcoded fashion.

I found out that each 'details' page simply had the company name appended to the end of the URL (example [page](https://www.startupranking.com/medium)). Since I already scraped the name of the company from the homepage. It was simply a matter of adding the `name` instance variable onto the end of the URL of the details page that I need information from. 

<h3>Waiting on the Scraper</h3>

I soon found out that the user would end up waiting on the scraper to load the information every time they wanted to be show the list of startups again. To fix this, I decided to create a `refresh` method. This way, if the user wants to see the list, and the instance variable already has a value, it will not scrape again; however, if the user types in 'refresh' it will call on the `refresh` method and re-scrape the page for the most up-to-date data. I found that this made the user experience much more fluid. 


<h3>In conclusion</h3>

Overall, I found this project to be quite the learning experience and test of patience. I also learned that scraping for data is sometimes not as easy as simply reaching in and grabbing a title, but can often be a long stretch of trial and error before you get the desired result.







