---
layout: post
title:      "Daydreaming of Rack"
date:       2018-07-30 18:33:28 +0000
permalink:  daydreaming_of_rack
---


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So the otherday after wrapping up my Sinatra project I realized I didn't understand much of the structure for setting up Sinatra. I mean I know how to get everything going by copying previous projects but I really couldn't explain much of why I was doing it. As I laid in bed running the setup in my head all I could think about was config.ru, rack, and app.rb. After half-an-hour of this I got on my computer and tried to execute my thoughts I quickly hit a wall and accepted the fact that I couldn't establish a connection to my browser from my IDE. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;After being humbled, I decided to re-read learn's lesson on rack and check out https://www.rubydoc.info/gems/rack/ to gain a different perspective and clean up holes in my thinking. This is what I got:

* Rack provides a **minimal, modular, and adaptable interface** for **developing web applications in Ruby**. By wrapping HTTP requests and responses in the simplest way possible, it **unifies** and **distills** the **API for web servers, web frameworks, and software** in between (the so-called middleware) **into a single method call**.

* Supported web servers:  The included handlers connect all kinds of web servers to Rack, which includes one that I am familiar. I see WEBrick pop-up when everything in my browser is working fine. 

* Supported web frameworks: There are many here just like web servers, the ones I'm most familiar with are Sinatra and Ruby on Rails.  

**Why should I use Rack?**

* **Convenience**. If you want to develop outside of existing frameworks, implement your own ones, or develop middleware, Rack provides many helpers to create Rack applications quickly and without doing the same web stuff all over:

* **Rack::Request**, which also provides query string parsing and multipart handling.

* **Rack::Response**, for convenient generation of HTTP replies and cookie handling.

* Rack::MockRequest and Rack::MockResponse for efficient and quick testing of Rack application without real HTTP round-trips.

**What's the deal with Rackup and config.ru?**

* Rackup is a **useful tool for running Rack applications**, which **uses** the **Rack::Builder** DSL **to configure middleware** and build up applications easily.

* Rackup **automatically figures out the environment** it is run in, and **runs your application as** FastCGI, CGI, or **WEBrick**—all from the same configuration.

* From my understanding and experimentation it seems that the file does not need to be named config.ru, but must have an .ru extension. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;With this information I opened my IDE, created a config.ru file and wrote the following. 

```
class Application

  def call(env)
    resp = Rack::Response.new
    resp.write "Hello World"
    resp.finish
  end

end

run Application.new
```

then I typed, 

```
gem install rack
```

followed by,

```
rackup config.ru
```

which output the following,

```
Your server is running at 165.227.31.156:35598
===================LOGS======================
Thin web server (v1.7.2 codename Bachmanity)
Maximum connections set to 1024
Listening on 0.0.0.0:9292, CTRL+C to stop
23.243.239.35 - - [30/Jul/2018:17:18:03 +0000] "GET / HTTP/1.1" 200 6 0.0036
23.243.239.35 - - [30/Jul/2018:17:18:03 +0000] "GET /favicon.ico HTTP/1.1" 200 6 0.0004
```

Originally the purpose of this thought exercise was to see how complicated I could get my program without using my ability to memorize name or look up, but through intuition to see how well I understand my knowledge. With that in mind I created a class to called Student to see if I could get a new Student to display on the browser. 

```
class Student
  attr_accessor :name

  def initialize(name:)
    @name = name
  end
end
```

and changed the call method to:

```
def call(env)
    joseph = Student.new(name: "Joseph")
    resp = Rack::Response.new
    resp.write "#{joseph.name}"
    resp.finish
  end
```

Sure enough it worked. From there I decided to see if I could add ActiveRecord to it, but once again I hit a wall. Do I need a Rakefile? or can I add ActiveRecord in my config.ru file? Again, I wanted to see how simple I could build up an applicaiton even if it's sloppy. I'll leave the answer to that for another post.





