---
layout: post
title:  "Implementing Authentication with Devise"
date:   2016-10-18 23:44:04 -0400
---


![](https://achievement-images.teamtreehouse.com/badges_Ruby_UserAuthentication_Stage1.png)

 Password-protected actions are something we experience everyday as users of software in our daily lives. Only allowing registered users in with a valid password is called “User Authentication.”

**Typical User Authentication Process**
1. Signup - create a new user profile with a Username, Password(Encrypted), e-mail, etc

2. Login - a user must sign in with their valid Username and Password which is then authenticated by matching the stored the username and password in the database, allowing the user access to the protected actions only if the given information matches the recorded values successfully. If not, the user will be redirected to the login page again. 


3. Access Restriction - create a session to hold the authenticated user ID after login, so navigation through additional protected actions can be done easily by just checking the userID in the current session.


4. Logout - allow the user to sign out and set the authenticated userID in session file to nil.

The Devise Gem is a flexible authentication solution for Rails. It allows developers to rapidly set up a fully functioning login system, and Devise gives you basically everything you need to solve the problem of authentication. Devise 4.0 works with Rails 4.1 onwards. Devise is based on Warden, which is a general Rack authentication framework created by Daniel Neighman.
Warden is designed to be lazy. That is, if you don’t use it, it doesn’t do anything, but when you do use it, it will spring into action and provide an underlying mechanism to allow authentication in any Rack-based application.


After adding it to your gemfile and running the bundle command to install it we run the generator:

```
$ rails generate devise:install
```

This will set up devise as well as output a set of instructions in the console to follow. You will need to configure Devise by settting up the default URL options for the Devise mailer in the enviornment. Such a configuaration in the config/environments/development.rb file would be"
```
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

Then Open up `app/views/layouts/application.html.erb` and add:
` 
<% if notice %>
  <p class="alert alert-success"><%= notice %></p>
<% end %>
<% if alert %>
  <p class="alert alert-danger"><%= alert %></p>
<% end %>
` 

An important place to to take a look is inside of the *initializer* that the generator will install because it will describe Devise's configuration options. For example:

```
# ==> Configuration for :validatable
# Range for password length.
config.password_length = 6..128

# Email regex used to validate email formats. It simply asserts that
# one (and only one) @ exists in the given string. This is mainly
# to give user feedback and not to assert the e-mail validity.
config.email_regexp = /\A[^@\s]+@[^@\s]+\z/
```

The above code found in config/initializers/devise.rb will validate for password length and e-mail format respectively.

After following these steps you will be able to use the Devise generator to add Devise to your models. 
```
$ rails generate devise User
 rake db:migrate
```
This command will create a User model and configure it with a series of default Devise modules, as well as configuring your routes file with the Devise controller. Then you may need to add additional configuration that your project might require.

All we need to do now is to add appropriate links for the user to be able to log in.
```
  <%= link_to("Sign Up", new_user_registration_path) %>
```


Devise will create some helpers that you can use inside your controllers and views. For example setting up a controller with user authentication add the following before_action:

```
before_action :authenticate_user!
```

Other helpful helpers that are commonly used are: `user_signed_in?`, `current_user`, `user_session`. These will verify if a user is signed in, return the current signed in user, and allow access to the session. 

After signing in a user, confirming the account or updating the password, Devise will look for a scoped root path to redirect to. For instance, when using a :user resource, the user_root_path will be used if it exists; otherwise, the default root_path will be used. This means that you need to set the root inside your routes:
```
root to: 'home#index'
```

 **Configuring Models**
 ```
 class User < ActiveRecord::Base
  devise :database_authenticatable, :registerable,
          :recoverable, :rememberable, :trackable, :validatable,
          :confirmable, :lockable, :timeoutable
 end
```

As previously mentioned the Devise method that is generated in your model is set to a default configuration but developers are able to custimize functionality to meet their specs. For example the Devise documentations give the following example of customizing the cost of the hashing algorithm with:
```
devise :database_authenticatable, :registerable, :confirmable, :recoverable, stretches: 12
```

The file located in /config/initializers/devise.rb is a great place to get more information on other options for configuring Devises modules.

**Configuring Views**
Since Devise is an engine, all its views are packaged inside the gem. These views will help you get started, but after some time you may want to change them. If this is the case, you just need to invoke the following generator, and it will copy all views to your application:
```
$ rails generate devise:views
```

If you have more than one Devise model in your application (such as User and Admin), you will notice that Devise uses the same views for all models. Fortunately, Devise offers an easy way to customize views. All you need to do is set config.scoped_views = true inside the config/initializers/devise.rb file.

**Configuring controllers**
If the customization offered to you at the views level is not enough, you can customize each controller by following these steps:

**1 **- Create your custom controllers using the generator which requires a scope:
```
$ rails generate devise:controllers [scope]
``` 

If you specify users as the scope, controllers will be created in app/controllers/users/. And the sessions controller will look like this:
```
class Users::SessionsController < Devise::SessionsController
  # GET /resource/sign_in
  # def new
  #   super
  # end
  ...
end
```


**2** - Tell the router to use this controller:
```
devise_for :users, controllers: { sessions: 'users/sessions' }
```


**3** - Copy the views from devise/sessions to users/sessions. Since the controller was changed, it won't use the default views located in devise/sessions.

**4** -  Finally, change or extend the desired controller actions.
```
class Users::SessionsController < Devise::SessionsController
  def create
    # custom sign-in code
  end
end
```

Resources:
https://launchschool.com/blog/how-to-use-devise-in-rails-for-authentication
https://github.com/plataformatec/devise
http://guides.railsgirls.com/devise















