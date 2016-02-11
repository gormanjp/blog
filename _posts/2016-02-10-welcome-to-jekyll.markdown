---
layout: post
title:  "CLI Gem"
date:   2016-02-10 15:50:25 -0500
categories: Learn Verified
---

I'm currently enrolled in online full stack web development bootcamp of sorts called Learn Verified.  I started with the program at the begining of the year and have slowly but steadily developed what feels like a pretty solid foundation for Ruby.  The program consists of a mix of written lessons, video lectures, test driven labs, and projects.  The first project that I completed was a Tic Tac Toe game that included an AI player and a command line interface to play the game.  

Here's the repo if you want to check it out:

The next project in the course was a bit more open ended.  The requirements were to build a ruby gem that scraped data from an external source and returned it via CLI.  It took me all of 4 minutes to decide what type of data my gem would be scraping.  Enter, college basketball.

This is the time of year that I start to get really into college basketball.  If I'm not coding or at work, I'm likely watching angry old men yell at 18-20 year olds because they missed a free throw.  It's awesome.  When there aren't any games on, I start looking at stats.  So naturally, this is what I decided to build my gem around.  

The gem scrapes from http://espn.go.com/mens-college-basketball/rankings and returns an up to date list of the top 25 teams in the nation.  At that point, the user can select a specific team from the list to see what their current record is.  Once the user has selected a specific team, they have the option to look up the latest tweet from the team or get info on their next match up.

One issue that I ran into was with the time listings for the upcoming matches.  When I went to scrape the times from the website, I was getting data that was consistently three hours off.  Scraping 8:00 PM from the site returned 5:00 PM, 1:00 PM returned 10:00 AM, etc.  I figured that this was some sort of time zone issue and even though I was seeing it as EST on the site, somehow when I scraped it, I was getting west coast time.  After a fair bit of googling I decided it might be easier to just build a quick workaround.

{% highlight ruby %}
time = info.search('div.time').text
if time.length == 7
	hour = time[0].to_i + 3
	time[0] = hour.to_s
	@schedule << time.gsub("AM","PM")
elsif time.length == 8
	hour = time[0..1].to_i - 9 
	time[0..1] = hour.to_s
	@schedule << time.gsub("AM","PM")
end
{% endhighlight %}

It's a bit sloppy, but it works.  The elsif portion accounts for 2 digit scenarios like 10:00 AM or 11:00 AM.  That way 10:00 AM doesn't become 40:00 PM.

Overall I have to say that I ended up enjoying this project more than I expected.  I found it really satisfying to build something that returns up to date info and dynamic content like most recent tweets.  I wanted to add more options and stats but more importantly, I need to keep learning.  

Here's the repo if you want to check it out:




