---
layout: post
title:      "Who or what is Barry?"
date:       2019-02-03 19:52:10 -0500
permalink:  who_or_what_is_barry
---


**There are three problems with the way news is done today:**

**1. There are no objective measures that can be represented numerically,** no widely accepted scoring system, for the accuracy, bias, and balance of news.

**2. Journalists and editors have emotions,** which unavoidably and implicitly affects the work product. (This is not a criticism of the profession of journalism but a statement of what I believe to be a fact.)

**3. Many people lack the awareness, time, motivation, and powers** of discriminatory thought to consciously look for bias and lack of balance and accuracy in a news piece and then seek out, select and read other high-quality articles from reputable sources on the same topic to get the most complete perspective on an issue.

**I predict that just as how today surgeons cannot make incisions** more precise than a robot can, in the future, a journalist will no longer be able to collect and report the news with more precision than an artificial intelligence can. For a time, the AI will need the journalist to oversee its activities and make ethical judgment calls, but eventually, the AI will be able to act completely and unerringly independently.

**Advances in cognitive technologies will make it possible** to solve the aforementioned problems and do no less than revolutionize how news is collected, created, and delivered in a way that helps unify humanity around an exceedingly sophisticated, robust, and reliable news source.

**I call my agent for achieving this vision** [Barry](https://github.com/adudley78/barry), simply because Barry sounds friendly, intelligent, and like someone dependable you can trust and count on to do the right thing. (To me, Barry sounds like a volunteer firefighter, a salt of the earth, straight-shooting midwestern type person with the highest moral character and unshakable values.)

**Imagine a world in which Barry, a centralized artificial intelligence** extended by a global network of AI journalists (JournoBots™️), makes it possible for everyone, regardless of language, literacy, or location, to have access to the absolute truth about what’s happening in the world. I’m talking about 100% accurate, unbiased, and balanced news for all people, everywhere on this planet and every other planet we decide to settle and live on as well.

**Now, I acknowledge this vision is huge and will seem to border on science-fiction** for some who are less initiated to AI and [its capabilities and potential](https://www.ynharari.com/book/21-lessons/). But I believe this (and much more!) will all be possible as the nascent field of [computational journalism](http://www.compjournalism.com/) evovles and the requisite technologies including artificial superintelligence come alive.

**All that said, since it’s early in my coding journey,** I lack much of the knowledge and many of the skills necessary to bring my longrange vision for Barry to fruition. I’ll need help from people with specialized knowledge (I’ve already begun recruiting) if I want to make significant progress on this in a reasonable timeframe.

**What I was able to do now, however, is write an early expression** of a Version 1.0 of Barry, a news article pseudo-analyzer, while meeting the requirements for my second major project for the Flatiron School’s full-time Immersive Software Engineering course in which I am currently enrolled.

**Approach**

**I wrote a web application, in Ruby on the Sinatra framework,** with the intention of following MVC architecture and the single responsibility principle. The app allows users to signup, login, and log out. Logged in users can submit news articles to Barry, a theoretical AI at this juncture, for pseudo-analysis.

**Each article instance is saved, objectified, persisted** in an SQLite database, and then pseudo-analyzed for accuracy, bias, and balance for a randomized score of 1-100%, with the pseudo-score for each article being returned to the user in a dashboard view via a custom pseduo_score_randomizer method I wrote.

**From their dashboard, a user can easily edit and delete** each article they’ve submitted to Barry as well as look at all the articles Barry has ever pseudo-analyzed. Objects of the class Article belong to a user and objects of the class User has many articles. For each of these classes, there is a corresponding table in the SQLite database and several columns corresponding to the attributes of each class. Instances of each class are persisted and represented as rows in one of the two the SQLite tables.

**Here is a breakdown of the application components.**

### Database

I used SQLite for my database and DB Browser for SQLite to visualize my tables and data while building and testing. Here is my schema.

```
ActiveRecord::Schema.define(version: 20190201140855) do

  create_table "articles", force: :cascade do |t|
    t.text    "title"
    t.text    "content"
    t.text    "pseudo_score"
    t.integer "user_id"
  end

  create_table "users", force: :cascade do |t|
    t.string "username"
    t.string "email"
    t.string "password_digest"
  end

end
```

### Config.ru

This file is where the application initializes. It loads the Ruby development environment, installing all the required libraries (gems), calling the Sinatra environment, and establishing a connection to the database using ActiveRecord, then mounting the required controllers. 

```
require './config/environment'

if ActiveRecord::Migrator.needs_migration?
  raise 'Migrations are pending. Run `rake db:migrate` to resolve the issue.'
end

use Rack::MethodOverride

# Mount master controller
run ApplicationController
# Mount additional controllers
use ArticlesController
use UsersController
use SessionsController
use RegistrationController
```

### Controllers

**I wrote five controllers for this web application:**

* Application - Root/route action and helper methods
* Registrations - Actions/routes related to registering and persisting a new User instance 
* Sessions - Actions/routes related to logging in, logging out, authenticating, establishing and clearing user sessions
* Users - Actions/routes related to the user dashboard
* Articles - CRUD actions/routes related to articles

### Models

**Two models were required for this application,** a User and an Article model. Using association macros inherited from the ActiveRecord codebase, I set Article instances to belong to a User and instances of a User to has many in the Article model. The User model also uses the has_secure_password from the bcrypt gem and validates a User instance on a username.

### Views

**For consistency and clarity, I tried to line up each view folder** and ERB file with their corresponding controller actions and routes. The HTML in the view files is simple and displays wrapped in a CSS layout courtesy of a gem called Corneal, which established my initial folder/file structure. I used the minimum possible code to create my views because demonstrating design skills was not the purpose of this project. However, I do appreciate visually beautiful and elegant applications, so I am in the process of implementing Twitter’s Bootstrap, a front-end framework, to deliver a basic and appealing design template.

**In addition to having a lot of fun while building this project,** I also learned some things:

* Impatience does not pay. TESTING along the way, at each step, does pay in a big way.
* It’s easy to get overwhelmed looking at a project as a whole, so I take the suggestion of Avi Flombaum, a founder of Flatiron and the lecturer in many of the prerecorded lectures we watch as part of the curriculum, which is to, while coding, keep moving the ball down the field, a few yards at a time. Chip away at it. Just think about what I need to do to make the next one or two things work. Get those things working and move on.
* Prioritized checklists of to-dos helped massively and created a much-needed sense of clarity and calm. I use [Things](https://culturedcode.com/things/) to be organized and to maintain a clear mind.
* Writing object associations and collaborations in Ruby manually came slowly to me. This project gave me the opportunity to write those same patterns in pry sessions while testing and I found that I was able to do so with much more proficiency and confidence than I was able to just a few weeks ago. A good feeling!
* Finally, I reconfirmed how practically minded I am. Building this project around something I’m deeply passionate about and committed to, Barry, fired me up. I was willing to work longer and harder and to go deeper than I would on some random idea that I didn’t feel a personal connection to. That’s just the way I’m wired.  


**Where I’d like to go next with this project:**

* I look forward to building out Barry’s front-end using Bootstrap initially while evolving the backend, possibly upgrading from Sinatra to the more powerful Rails which I believe is our next major project at Flatiron.
* I want to practice writing tests in RSpec and Capybara.
* I want to read and completely understand the ActiveRecord, Sinatra and Rails codebases.
* I want to become more knowledgeable about how databases work.
* I want to dive a little deeper into how Rack works to act as an interface between web applications and HTTP request/response and cement my knowledge of how the web works.
* There are gems and APIs out there available for use that have some AI capabilities for text analysis, so I’d like to select some of these to test for going from article pseudo-analysis to real, meaningful analysis with Barry.
