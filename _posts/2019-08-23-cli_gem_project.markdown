---
layout: post
title:      "CLI Gem Project!"
date:       2019-08-23 11:59:09 +0000
permalink:  cli_gem_project
---

### Best Hikes in Norway


When brainstorming ideas for my CLI project, I thought about how often my friends and family are looking for new hikes to try out here in Norway - my project idea was born! I found a website with some of the best hikes in Norway and got straight to scraping. I split my scraper class into three methods, each getting progressively more detailed information. I decided to scrape name, location, distance, difficulty, duration, and url for each of the 12 hikes. 

```
class BestHikes::Scraper

  def get_page
    Nokogiri::HTML(open("https://outtt.com/en/guides/225/12-best-hikes-norway"))
  end

  def get_hike
     self.get_page.css("div.columns.is-multiline div.column.is-one-third-tablet")
  end

  def make_hikes
    get_hike.each do |h| 
      name =  h.css(".sort-title").text
      location = h.css(".has-text-grey").text
      distance = h.css(".sort-distance").text
      difficulty = h.css(".sort-difficulty").text
      duration = h.css("span:nth-child(6)").text.gsub(/\s+/, "")
      url = h.css("a").attribute("href").text
      website = "https://outtt.com" << url
      BestHikes::Hike.new(name, location, distance, difficulty, duration, website)
    end
  end
end
```

After parsing the details I wanted for each hike, I started working on the CLI and Hikes classes simultaneously, as this helped me figure out how I wanted the user's experience to flow. I wanted the user to be greeted and shown a list of hikes with their locations, and from there to be able to select a hike for more information. The user would then be asked if they want to return to the hikes list to select another hike. This loop continues until the user indicates that they no longer want to see more hikes.

```
class BestHikes::CLI

  def call
    BestHikes::Scraper.new.make_hikes # call on Scraper class to get hikes
    puts "Best Hikes in Norway!".red.on_blue.bold
    display_hikes
  end

  def display_hikes
    puts "Here are some of the best hikes in Norway listed by name and location:".red
    puts ""
    BestHikes::Hike.hike_list # call on Hike class to get list of hikes
    puts ""
    puts "Please enter the number of the hike you'd like more information on (1-12):".red

    input = gets.strip.to_i
    if input > 12
      puts "Oops! That hike doesn't exist (yet) - please enter a number between 1 and 12".red
      input = gets.strip.to_i
      hike = BestHikes::Hike.find(input)
      BestHikes::Hike.hike_info(hike)
    else
      hike = BestHikes::Hike.find(input) # call on find method in Hike class & assign to hike variable
      BestHikes::Hike.hike_info(hike)
    end

    puts "Would you like to see more hikes? Please enter Y or N!".red
    input = gets.strip.downcase
    if input == "y"
      display_hikes
      elsif input == "n"
      puts "Thank you for your interest in hikes in Norway!".red
      exit
    else
      display_hikes
    end
  end
end
```

Next I needed to build out the methods in the Hike class to make this happen. I initialized each instance of a new hike with the hike details, which all have reader and writer methods through attribute accessor. I then used class methods to find the hike selected by the user, iterate through the hikes with `@@all`  and `each.with_index(1) `  to create my list of hikes, and finally a class method to display all the details of the hike selected by the user.

```
attr_accessor :name, :location, :distance, :difficulty, :duration, :website

  @@all = []

  def initialize(name, location, distance=nil, difficulty=nil, duration=nil, website=nil)
    @name = name
    @location = location
    @distance = distance
    @difficulty = difficulty
    @duration = duration
    @website = website
    @@all << self
  end

  def self.all
    @@all
  end

  def self.find(id)
    self.all[id-1]
  end

   def self.hike_list
    @@all.each.with_index(1) do |hike, index|
      puts "#{index}. #{hike.name} - #{hike.location}"
    end
  end

  def self.hike_info(hike)
    puts "#{hike.name} - #{hike.location}"
    puts ""
    puts "Distance: #{hike.distance}"
    puts "Difficulty: #{hike.difficulty}"
    puts "Duration: #{hike.duration}"
    puts "Website: #{hike.website}"
  end
end
```

I took a break from this project for awhile (do not recommend!), and moved on with the curriculum when I felt stuck. Revisiting this code was both challening and motivating, because I realised how much I'd learned since I first started it.








