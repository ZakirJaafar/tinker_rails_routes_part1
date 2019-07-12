## Tinker - Rails Routes - part 1

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



==Second== I created a new folder `test` within the View folder and also created a new `show.html.erb`file within that folder `app/views/test/show.html.erb` In that file `show.html.erb` file I added this code:

```
<%= "hello world" %>
```



==Third== I also created a new file called `test_controller.rb` within the Controllers folder `app/controllers/test_controller.rb` Within this `test_controller.rb` file I added this code:

```
class TestController < ApplicationController
def show
end
end
```

The `get '/test/', :to => 'test#show'`  code is to modify the Rails Router part of the MVC. The above code will give the `routes` below screen shot:


![](http://ww4.sinaimg.cn/large/006tNc79gy1g4rhus7t6yj30pa05vt92.jpg)

The code above `get '/test/', :to => 'test#show'` will allow you the URL `localhost:3000/test` Which means without `localhost:3000/test/show` and only `localhost:3000/test` is enough to call the View file `show.html.erb` with "Hello World" rendered. 

Whereas below code in the`routes.rb` will insist that the URL be `localhost:3000/test/show`

```
get 'test/show'
```

The code `get 'test/show'` will insist the URL be `localhost:3000/test/show`(emphasis `/show` towards the end) since the `routes` is different:

![](http://ww2.sinaimg.cn/large/006tNc79gy1g4rhbuwscsj30pj04rt95.jpg)

It would be useful to have without `/show` for the URL when you want to display let's say the Homepage.

So for now let's say in our `routes.rb` we have`get 'test/show'`. Now it's best to explain the high level sequence of Rails Routing. 



![](http://ww3.sinaimg.cn/large/006tNc79gy1g4rioel8ovj30ro02rmx8.jpg)



When you enter the URL address in the browser or click some button where the user is calling to specific URL address, Rails server (after DNS resolved then pass to Rails) will identify the entered URL address and match with a specific line within the `routes`. There's Rails backend function which I don't want to confuse the reader. Once it found a match it will first call the `Verb` of the `routes` table. In this example it's the `GET` Verb (this is at ==No. 1== with the screen shot above). It will `GET` (more like it will **READ**) the corresponding `controller` (which is `test._controller.rb`) since the `routes` format shows `/test/show(.:format)` (emphasis the word `/test/` and this is at ==No. 2== with the screen shot above). 

|   CRUD Actions   |  HTTP Actions    |
| ---- | ---- |
| Create | PUT/POST |
| Read | GET |
| Update | POST/PUT |
| Delete | DELETE |

It will also **READ** the corresponding `controller` and corresponding `actions` based on the URI Pattern `/test/show(.:format)` `routes` table  (emphsis the word `/show` and this is at ==No. 3== with the screen shot above) 

Rails also put in memory of the URL content at  ==No. 1== and ==No. 2== screen shot above. Hence, `routes.rb` file will scrap the URL and put in memory

Why does Rails need to put in memory? So that it can refer to them when triggering ==No.1== and ==No.2==.  In this example of URL `localhost:3000/test/show`,  `test` as a parameter (`:controller` parameter) and `show` as another parameter (`:action` parameter). Rails will put these in memory plus if there's any other specific parameters.  In short, Rails will look at the value of the param [:controller] and use it to decide which type of `controller` it needs to call. Rails will also look at the value of the param [:action] and use it to decide which type of action within the `controller`it needs to call.

In our exercise, Rails will put in memory parameter [:controller] `test` and parameter [:action] `show` As shown in the table below 

| NAME        | VALUE   |
| ----------- | ------- |
| :controller | test   |
| :action     | show |

The first sequence within that memory of the table above is to call the para [:controller], Which is the file `app/controllers/test_controller.rb` (this is ==No. 3== with the screen shot above ). This file has the convention Rails naming <controller value name>_controller.rb. As shown in the screen shot below. 

![](http://ww1.sinaimg.cn/large/006tNc79gy1g4rlq9clm1j30ra0gi766.jpg)

Then, Rails memory of the parameters will trigger the [:action] param, meaning it will look for the function/action `show` within the `test_controller.rb` file. The action/function `show` can be seen in the screen shot above. The function/action `show` is empty, if it's not empty it will run any logic within this function. What ever the output of this `show` function/action it will put in memory too. Then the `routes` says `test#show` (emphasis on the `#show`) Which means it will call `app/views/test/show.html.erb` file. So what ever in memory after running that function/action at `test_controller.rb` will be used for the file `show.html.erb`. In our exercise `show.html.erb` (screenshot below) will display on the browser `hello world` texts. Actually the View file `show.html.erb` will pass it through the `controller` only then browser get to render with the correct URL address on the browser. There's more thing that goes on at the webserver level but it's enough to know the highlevel processes. 

![](http://ww3.sinaimg.cn/large/006tNc79gy1g4rm9wqu5qj30k50g0abi.jpg)

Screenshot be of what got triggered at the terminal when Rails server was running after URL entered at the browser:

![](http://ww3.sinaimg.cn/large/006tNc79gy1g4w4iari16j311q0aymzo.jpg)

Another example:

User entered address in the URL and it find if there's any parameters within the URL. Such as `http://localhost:3000/rooms/10/listing`. In this example of URL, there's an ID of 10 as parameter, `rooms` as another parameter (`:controller` parameter) and `listing` as another parameter (`:action` parameter). Rails will put these in memory plus if there's any other specific parameters before calling the `controller` `rooms` and triggering `action` method/function `listing`


| NAME        | VALUE   |
| ----------- | ------- |
| :id         | 10      |
| :controller | rooms   |
| :action     | listing |




To recap the `routes` again of our exercise:

![](http://ww3.sinaimg.cn/large/006tNc79gy1g4rioel8ovj30ro02rmx8.jpg)


In short, the rails routing system knows how to turn a visitor's entered URL into a controller/action sequence. It also knows how to spit out URL strings based on what you specified.


### Where: GitHub Repo

The GitHub repo is was pushed from my local. Hopefully you can fire the Rails server after you have cloned in your local. I installed Rails without test and turbolinks. I used Postgresql instead. I probably added stuff not necessary for this demo. What's important is that I got my point across on Rails Routes.  

### When: Date Created & Updated

**Created**:  6th July 2019

**Updated**: 12th July 2019
