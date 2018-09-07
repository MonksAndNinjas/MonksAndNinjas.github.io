---
layout: post
title:      "URL Helpers Research"
date:       2018-09-07 18:52:45 +0000
permalink:  url_helpers_research
---


Currently I am in the middle of my Rails section for Learn and I noticed some url helpers that I'm not familiar with so I decided to look at URL Helpers in the Rails guide. Below you'll find some information that I felt would be helpful to know that they exist. Hopefully you find this as helpful as I did.

## link_to
*The first two are pretty straight forward and should be familiar.*

```
link_to "Profile", profile_path(@profile)
# => <a href="/profiles/1">Profile</a>
```

```
link_to "Profile", @profile
# => <a href="/profiles/1">Profile</a>
```

*and this one as well.*

```
link_to "Profiles", profiles_path
# => <a href="/profiles">Profiles</a>
```

*When name is nil the href is displayed.*

```
link_to nil, "http://example.com"
# => <a href="http://www.example.com">http://www.example.com</a>
```

*linkto can also be used with a block.*

```
<%= link_to(@profile) do %>
  <strong><%= @profile.name %></strong> -- <span>Check it out!</span>
<% end %>
# => <a href="/profiles/1">
       <strong>David</strong> -- <span>Check it out!</span>
     </a>
```

*Classes and Id's can be used on links as such.*

```
link_to "Articles", articles_path, id: "news", class: "article"
# => <a href="/articles" class="article" id="news">Articles</a>
```

*and we have the familiar delete link.*

```
link_to("Destroy", "http://www.example.com", method: :delete)
# => <a href='http://www.example.com' rel="nofollow" data-method="delete">Destroy</a>
```

*One could also add custom attributes by using data option.*

```
link_to "Visit Other Site", "http://www.rubyonrails.org/", data: { confirm: "Are you sure?" }
# => <a href="http://www.rubyonrails.org/" data-confirm="Are you sure?">Visit Other Site</a>
```

## link_to_if

```
<%= link_to_if(@current_user.nil?, "Login", { controller: "sessions", action: "new" }) %>

# If the user isn't logged in...
# => <a href="/sessions/new/">Login</a>

<%=
   link_to_if(@current_user.nil?, "Login", { controller: "sessions", action: "new" }) do
     link_to(@current_user.login, { controller: "accounts", action: "show", id: @current_user })
   end
%>

# If the user isn't logged in...
# => <a href="/sessions/new/">Login</a>
# If they are logged in...
# => <a href="/accounts/show/3">my_username</a>

```

## link_to_unless
*Here are a couple of examples.*

```
<%= link_to_unless(@current_user.nil?, "Reply", { action: "reply" }) %>

# If the user is logged in...
# => <a href="/controller/reply/">Reply</a>

<%=
   link_to_unless(@current_user.nil?, "Reply", { action: "reply" }) do |name|
     link_to(name, { controller: "accounts", action: "signup" })
   end
%>

# If the user is logged in...
# => <a href="/controller/reply/">Reply</a>
# If not...
# => <a href="/accounts/signup">Reply</a>
```

## link_to_unless_current

```
<ul id="navbar">
  <li><%= link_to_unless_current("Home", { action: "index" }) %></li>
  <li><%= link_to_unless_current("About Us", { action: "about" }) %></li>
</ul>
```

*or as a block.*

```
<%=
    link_to_unless_current("Comment", { controller: "comments", action: "new" }) do
       link_to("Go back", { controller: "posts", action: "index" })
    end
 %>
```

## current_page?

*I thought these would be helpful in getting info about a page.*

```
#Let's say we're in the http://www.example.com/shop/checkout?order=desc&page=1 action.

current_page?(action: 'process')
# => false

current_page?(action: 'checkout')
# => true

current_page?(controller: 'library', action: 'checkout')
# => false

current_page?(controller: 'shop', action: 'checkout')
# => true

current_page?(controller: 'shop', action: 'checkout', order: 'asc')
# => false

current_page?(controller: 'shop', action: 'checkout', order: 'desc', page: '1')
# => true

current_page?(controller: 'shop', action: 'checkout', order: 'desc', page: '2')
# => false

current_page?('http://www.example.com/shop/checkout')
# => true

current_page?('http://www.example.com/shop/checkout', check_parameters: true)
# => false

current_page?('/shop/checkout')
# => true

current_page?('http://www.example.com/shop/checkout?order=desc&page=1')
# => true
```

And there it is I hope you liked the article and thanks for stopping by.
