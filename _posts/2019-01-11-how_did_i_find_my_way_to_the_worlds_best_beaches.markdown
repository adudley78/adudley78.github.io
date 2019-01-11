---
layout: post
title:      "How did I find my way to the World's Best Beaches?"
date:       2019-01-11 15:50:28 +0000
permalink:  how_did_i_find_my_way_to_the_worlds_best_beaches
---


**I believe in keeping things fun, simple, and low-stress** whenever possible because often my nature takes me in the exact opposite direction and that, I’ve found, is not healthy or productive state for me.

**So when I began this Ruby CLI project** I looked at the [World’s Best Restaurants CLI app](https://github.com/cjbrock/worlds-best-restaurants-cli-gem) example given in the curriculum at Flatiron, where I’m enrolled in the full-time immersive software engineering program, and shared it with my wife. She said I should do that but with beaches because we love the beach and live at the beach.

**I thought that was a great idea, simple, and doable** but then my serious side kicked in and I thought I should instead do an app that scraped remote job sites. That’s more appropriate domain I thought because it’s more serious and professional and a remote job is an ideal scenario for me when I land a job in this field.

**Naturally, when I do the opposite of what I believe in** I get a less than desirable result. After going through two remote job sites that proved, frustratingly, to not be scrapable, I abandoned that topic and moved on to the original beach idea, which I should have embraced in the first place. (Life Lesson: Always listen to your wife!)

**So I restarted my project but ran into scraping trouble** yet again with the first best beaches website I chose and had to abandon that one as well. (This whole experience made me wish I had chosen an API as a data source over scraping!) Since I was stuck, I sought help from my cohort lead and he helped me find a site written in a way that would accommodate scraping. 

**Finally, I was ready to build [my CLI app in Ruby]**(https://github.com/adudley78/worlds-best-beaches-cli-project-122018).

**I began with a module, WorldsBestBeaches**, that contains two classes, Beach and CLI. The CLI class is responsible for delivering the user experience at the command line and the Beach class is responsible for delivering the scraped, objectified beach data to the CLI class. (Refactor opportunity: Create a Scraper class and move all related methods into it.)

```
module WorldsBestBeaches
  VERSION = "0.1.0"
end
```

**In the CLI class, I designed the user interface.** It begins with a call method to initiate the scrape and methods needed upon program execution. As I learned, it was important to scrape the data at this point in the lifecycle as opposed to when the method that prints the menu of beaches is called so as not to have to scrape the data every the menu is called.

```
def call
    WorldsBestBeaches::Beach.today # call the scrape
    list_beaches
    menu
  end
```

**In the Beach class, I initialize a new beach object** with three attributes then add each instance to an empty array assigned to a class variable, @@all. (Refactor opportunity: Use mass assignment with the .send method.)

```
def initialize(name=nil, location=nil, more_info=nil) # refactor with mass assignment pattern
    @name = name
    @location = location
    @more_info = more_info
    @@all << self
  end
```

**In the Beach class method responsible for scraping,** I had to use a group of [smelly](https://en.wikipedia.org/wiki/Code_smell) if/else conditional statements because there were numerous formatting issues with the website that needed to be dealt with element by element in order to deliver correct and clean output to the user. (Refactor opportunity: Use a case statement.)

```
def self.scrape_tripadvisor
    doc = Nokogiri::HTML(open("https://www.coastalliving.com/tripadvisor-best-beaches-world"))
    doc.search('.glide-slide.image-slide').each.with_index do |b, i|
      # refactor with case statement
      if i == 0
        location = b.search('.glide-slide-desc p a strong').text.split("!")[1][0..15]
      elsif i == 1
        location = b.search('.glide-slide-desc p a strong').text[0..35]
      elsif i == 4
        location = b.search('.glide-slide-desc p a strong').text[0..22]
      elsif i == 5
        location = b.search('.glide-slide-desc p a strong').text[0..17]
      elsif i == 12
        location = b.search('.glide-slide-desc p a strong').text[0..19]
      elsif i == 13
        location = b.search('.glide-slide-desc p a strong').text[0..29]
      elsif i == 14
        location = b.search('.glide-slide-desc p a strong').text[0..25]
      elsif i == 18
        location = b.search('.glide-slide-desc p a strong').text[0..19]
      elsif i == 20
        location = b.search('.glide-slide-desc p a strong').text[0..33]
      elsif i == 21
        location = b.search('.glide-slide-desc p a strong').text[0..15]
      elsif i == 22
        location = b.search('.glide-slide-desc p a strong').text[0..16]
      elsif i == 23
        location = b.search('.glide-slide-desc p a strong').text[0..31]
      else
        location = b.search('.glide-slide-desc p a strong').text
      end
      name = b.search('h3').text.strip.sub!( /\A.{3}/m, "" ).gsub(/\W/, ' ').strip
      if i == 1
        more_info = b.search('div.glide-slide-desc p')[2].text
      else
        more_info = b.search('div.glide-slide-desc p').last.text
      end
      self.new(name, location, more_info) # instantiate new beach objects from scraped data with three properties
    end
  end
```

**The last problem I had to solve to get Version 1.0** of this app to where I wanted it was unexpected and stumped me for a bit. The numbered list of beaches was displaying as 25 to 1 and when I tried to reverse the order at the .each iterator in the CLI class, the order of the more info attribute data was also reversed. (Note: I wanted to reverse the order because I thought it would look strange to the user to see a list 25 through 1 when we’re used to seeing 1 through the larger number.)

**Recruiting a partner to help me think through the problem,** I tried implementing variations on a counter approach in the CLI class to change the order of the numbering without success. In a flash-moment of inspiration, I wondered what would happen if I simply called reverse on the class variable and array of beach objects, @@all. I implemented this and it worked! I couldn’t have been more astonished not only that it worked but that I thought to try it.

```
def self.all
    @@all.reverse # refactor with separate method that reverses the order
  end
```

**This was a very exciting moment for me** where I felt at my most capable, and a moment in which the balance tipped from frustration to fun! And that, by the way, is a metaphor I’ve come up with to describe the feeling of programming; it’s like a scale or teeter-totter with fun on one side and frustration on the other. And sometimes the feeling is right in the middle and at other times it’s more to one side than the other. Basically, I’ve found that I have to be willing to work through frustration to get to the fun part. That’s the mental game of programming for me.

----------------

**The next steps with this project to upgrade and refactor are to:**

* Build out a submenu method that allows the user to optionally get a clickable link to learn even more about each beach 
* Move scraper methods into a Scraper class to adhere to the single responsibility principle
* Break out code from methods that do not follow single responsibility into new, separate methods
* Improve the formatting by adding more spaces and colors to make the user interface more pleasing to the eye
* Find out, with some user testing, what else a user might want to do with the app and implement a prioritized list of meaningful upgrades
