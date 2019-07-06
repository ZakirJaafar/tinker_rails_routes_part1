## Tinker - Rails Routes

### Intro

These notes were created as part of my notes in my own words trying to understand certain concepts. This time it's on Rails Routes. Before this I sort of understood the overview of MVC Rails Architecture but not in depth. I went through many articles and app tutorials, app tutorials not specifically on Rails Routes, explaining on Rails routing system but I never took the effort in explaining it in depth of what I understood. As usual, there's alot more to learn. I am sure I will continue to update this as time goes by and refer these notes. 

The best way to learn (re-learn) is to clone the repo to your local, run Rails server and read these notes. Re-learn The Rules & Concept. Practice on the Rules & Concept. Break the Rules & re-Conceptualize



> P.S. The original copy of this aricle, is part of a chapter from Zakir's markdown Ruby Coding Notes (by now 59050 Words ) and pasted in `README` GitHub Repo `tinker_rails_routes`



> P.P.S. Please don't take these notes and my repo as true and error free. I am far from an expert. Please correct me if any of these are wrong. This is just merely my way of understanding my own thoughts, so that I can refer, and hopefully improve my understanding of the topic :)

### What: Rails Routes (the concept)



### How: My Understanding on Rails Routes

I am going to tackle the basic first and forget for now the inner parts of Rails. I am also going the manual way rather than use Rails `generator`. 

First let's dwell on the MVC Rails architecture. The simpler version as below (image from https://medium.com/@pattyjburns/a-primer-on-ruby-on-rails-for-product-managers-5b4f8e28b3ae)

![MVC Rails Architecture](https://miro.medium.com/max/700/1*SIW0API8ctEEyVbZ2V4KIg.png)

On the surface it is enough know about Rails Routes using `View`, `Controller`, and `Route` part of the MVC. The normal way is also to include `Model` part of the MVC but we are not going to do that in this exercise. 

Once I have installed the simple Rails app, ==First== I added the below code to the file `routes.rb` 

```
get '/test/', :to => 'test#show'
```



==Second== then I created a new folder `test` within the View folder and also created a new `show.html.erb`file within that folder `app/views/test/show.html.erb` In that file `show.html.erb` file I added this code:

```
<%= "hello world" %>
```

==Third== then I also created a new file called `test_controller.rb` within the Controllers folder `app/controllers/test_controller.rb` Within this `test_controller.rb` file I added this code:

```
class TestController < ApplicationController
def show
end
end
```



The `get '/test/', :to => 'test#show'`  code is to modify the Rails Router part of the MVC. The above code will give the `routes` below screen shot:

![tinker rails routes](/Users/ZakirJaafar/Dropbox/Ruby Coding Notes/tinker rails routes.png)

The code above `get '/test/', :to => 'test#show'` will allow you the URL `localhost:3000/test`Which means without `localhost:3000/test/show` and only `localhost:3000/test` is enough to call the View file `show.html.erb` with Hello Word rendered. 

Whereas below code in the`routes.rb` will insist that the URL be `localhost:3000/test/show`

```
get 'test/show'
```

The code `get 'test/show'` will insist the URL be `localhost:3000/test/show`since the routes is different:



![image-20190706232319375](/Users/ZakirJaafar/Library/Application Support/typora-user-images/image-20190706232319375.png)

### Where: GitHub Repo

The GitHub repo is was pushed from my local. Hopefully you can fire the Rails server after you have cloned in your local. I installed Rails without test and turbolinks. I used Postgresql instead. I probably added stuff not necessary for this demo. What's important is that I got my point across on Rails Routes.  

### When: Date Created & Updated

**Created**:  6th July 2019

**Updated**: 
