---
layout: post
title:      "My Sinatral Recipe App"
date:       2020-09-20 20:13:03 +0000
permalink:  my_sinatral_recipe_app
---


I must say that although working on the Sinatra project was definitely more chalenging, it was more enjoyable too. It seemed for me that there was a flow to the app and I could more intuitively predict what the next step should be - comparet to the CLI. For this assessment I'll be creating a CRUD, MVC app using Sinatra. This app should be a custom app that is created to organise my kitchen drawer full of printed recipes. 

I am going to use a gem called Corneal which you can look up here - https://github.com/thebrianemory/corneal. Corneal is basically a generator for Sintra to quickly build in files. If you dont have it all you need to do is run 'gem install corneal'. to scafold my project I am going to run 'corneal new sinatra-recipe-app' in the terminal. When you open your app you will see a structure that is familiar - MVC. config.ru is the file that allow us to build the app on top of rack. This is also where I mounted my controller and added 'use Rack::MethodOverride' which allows me to send patch and delete requestes. Very important step. The user is able to create and account which adds their info to a database including a secure password using the bcrypt gem. The users have many recipes and the recipe belong to the user. I would defintely suggest checking out the learn video project live build-ins, there were a few and I found them to be very useful. 


 My Sinatra App

User

I am going to build a recipe app where a User can create recipe entries. 

 A user will be able to:
- Signup
- Login
- Logout

As a user, I will be able:
- Create a recipe entry
- See all my recipe entries
- Edit my recipe entries
- Delete my recipe entries

Models:
1. User
2. Recipe entry

1. User Model
Attributes:
-name
-email
-password(if I use bcrypt this will be the password_digest in the DB)


2. Recipe Entry Model
Attributes:
-title
-ingredients
-content
-user_id <= this will be the foreign key

The User has_many :recipe_entries
A Recipe entry belongs_to :user

MVP
-Users can signup, login, logout, create recipe entries, edit their own entries and view their entries.

Stretch Goals:
-CSS
-include a join model - include a Recipe model where a user can categorise the recipe entries.

Here comes Rails! :-)

