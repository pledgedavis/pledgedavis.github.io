---
layout: post
title:      "Sinatra Portfolio Project"
date:       2020-04-12 12:31:48 +0000
permalink:  sinatra_portfolio_project
---


For this project I figured that I should create an app that allows you to adopt and name a dog as if it were a child. Which I feel is pretty neat since you're able to create an account by signing up and then access that account with a email, username and password all from your home! Then you would proceed to looking at the dogs we currently have available for adoption and choose from that list of which dog it is that you would like. I came up with the idea of dog adoption because there are currently over 600 thousands Dogs that get euthanized each year because the shelters are too full and not enough peple are adopting. So I came to the conclusion that it would be pretty cool to be able to sit at home and choose a pet you would like to save from over crowded shelters.

The app uses two migration tables which consists of a User and Dogs table to keep track of the attributes my Users and Dogs will have so they would be able to be interacted with. And also a bcrypt gem was installed to be able to store the users password in the database but in a way that only the user would know what it is which allows me to set an attribute on the users table as a string of `password_digest`.
```
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |p|
      p.string :username
      p.string :email
      p.string :password_digest #uses bcrypt gem and encrypts password 
    end
  end
end
```

```
class CreateDogs < ActiveRecord::Migration
  def change
    create_table :dogs do |p|
      p.string :name
      p.string :second_name
      p.integer :user_id
    end
  end
end
```

My project also uses *Helpers* to keep track of which users are logged in and the current session of the user.

```
class Helpers
#this helpers class maintains neatness throughout my application by defining usable instance methods in this file 
 def self.current_user(session)  
   User.find_by(id: session[:user_id]) #uses the sessions hash to find current user by id
 end

 def self.logged_in?(session)
    session[:user_id] ? true : false #method checks if users has an id because if so the user is logged in
 end
end

```

My helpers class is consisted of instance methods which create neatness and functionability throught the whole app by using the session hash as an arguement and keeping track of the current user with `:user_id` also checking if the user is logged in or not because if not logged in you should not be able to use or manipulate any of the dogs until an account is made or logged in to. the logged in method just checks if the user has a `user_id` because if so the method will then return a boolean value of true and false if not.

Then my content is then displayed throught my erb files inside of my views folder with the help of my Users and Dogs controllers which also helps control what information is displayed by using get request as well as post request that allow the user to CRUD actions.


