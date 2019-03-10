---
layout: post
title:      "Want to track your open source contributions?"
date:       2019-03-10 18:29:10 +0000
permalink:  want_to_track_your_open_source_contributions
---


**As a student more than halfway through** the full-time online immersive software engineering program at Flatiron School, I’ve already been on a couple of job interviews. In my first interview, I was given the following paraphrased advice by a VP of Software Engineering:

**“Since you’re early in your career as a developer,** it would be good to find some open source projects with issues to fix or features to build. If it’s an issue, try to fix it. If it’s a feature, try to build it. It’s ok if you don’t generate a pull request. Just make your best attempt so a potential employer can see your approach to problem-solving on a codebase that’s unfamiliar to you.”

**In the spirit of that advice, I started looking into opportunities** to contribute to open source projects. There are a lot of resources out there where you can find projects appropriate for all skill levels but I found them lacking in ease-of-use and elegance. So when it came time to decide what app to build for [my Ruby on Rails project](https://github.com/adudley78/flatiron-rails-project-022219) at Flatiron, I decided on an app for developers like me who might want to track their contributions.

**I call it Contribution-U or ConU for short.** To start, I borrowed the CSS from an open source project called [ToDoMVC](http://todomvc.com/). It’s a pretty simple yet elegant design template for any web app where you’re going to have lists of lists. ConU has three main classes/models: User, Project, and Issue. A Project is an open source project and an Issue is a bug or problem you want to try and fix and also want to track.

**In the future, I’d imagine connecting ConU to the GitHub API** and possibly others whereby projects and issues could be imported, searched through and selected by a user. As it stands now, however, a User has to enter their own projects and issues manually. These projects and issues, along with the instances of the User object, are persisted in an SQLite database and associated with one another using ActiveRecord.

**I really enjoyed working with Rails on this project** and I’m feeling strongly that I’ll specialize in Ruby on Rails going forward as I really like the depth and breadth of the framework and how it encapsulates and extends the functionality of Ruby. It’s fun for me to learn how to do things more succinctly with the myriad helper methods available through Rails. One in particular that I enjoyed learning about and using in this project is the scope helper for defining a method scoped to a model.

**Generally, I enjoy writing apps in Ruby on Rails** because of how powerful the language and framework are and the elegance of the MVC structure. I also like the community aspect of Ruby plus all the gems that are available to do different tasks though I’m also a little cautious in implementing gems when I don’t fully understand what’s happening under the hood. For example, I chose not to implement Devise on this project (I’ve since implemented it on another) because it seems like a very robust library and I didn’t feel like I had the time to get comfortable with it.
