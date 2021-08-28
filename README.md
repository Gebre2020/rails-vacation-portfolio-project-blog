# rails-vacation-portfolio-project
 
  - Rails Vacation Portfolio Project by Gebremeskel Gebrehiwot attending Flatiron School

My third Flatiron project assignment was to build a rails app from scratch. The project is about creating a location where the user can make trip budget within the list of locations or make a trip budget with a new location.
My app is called, vacation-rails-project, has many-to-many relationships. The app has user to signup and a sessions to login, after sign up or login the user able to access locations to create city and country.
To start the project,  I run 'rails new vacation-rails-project' in my terminal. I used a 'Rails generator resources', which creates a bunch of folder and files for users, locations, trips, & travels. 

# Prerequisites/Installation
I added 'gem' on Gemfile:
gem 'bcrypt', '~> 3.1.7'
gem 'omniauth'
gem 'omniauth-google-oauth2'
gem 'omniauth-rails_csrf_protection'
gem 'dotenv-rails'
Run bundle install
Run rails db:create and rails db:migrate
Run rails s to start the application

# Models
The project app is built with Ruby on Rails and follows the basic MVC pattern. There are four models: User,Location,Trip,and Travel.
First I created the relationships between the model class.

  class User < ApplicationRecord
      has_many :locations
      validates :email, presence: true, uniqueness: true
      validates :username, presence: true
      has_secure_password 
  end

  class Location < ApplicationRecord
    belongs_to :user
    has_many :trips
    has_many :travels, through: :trips
    validates :city, presence: true
    validates :country, presence: true
  end
  
  class Trip < ApplicationRecord
    belongs_to :location
    belongs_to :travel
    validates :budget, numericality: {greater_than: 0, less_than: 15000}
  end

  class Travel < ApplicationRecord
      has_many :trips
      has_many :locations, through: :trips
      validates :name, presence: true
      validates :address, presence: true
  end

I also added basic ActiveRecord validations for most things to require input of the group model to validates the attributes. I run rails db:migrate in the terminal to update db/schema.rb file to match the up-to-date structure of  database. 
A sample seed file can be created by running "rake db:seed". The db/seeds.rb file can be modified the associations of tables in database. I checked the relationships with running rails console in the terminal.

In the models I created the scope methods, reasonable validations,  has_secure_password in users file model, including signup, login, logout, and passwords, authentication along with Omniauth to allow login using google service.
 
Also I make a nested routes with the appropriate RESTful URLs with a nested new index or show routes with form that relates to the parents resource. I make the form to display validation errors messages describing the validation failures within the view. I make a lot of partial views to avoid dupulicated codes and the application to be 'DRY' by using layouts, partials, helpers and refactoring.

# Controllers
There are five (locations, sessions,travels, trips, and users) controllers. The controllers implement RESTful routes and more importantly nested routes.  I built a Sessions controller to deal with login and logout logic. I wanted user to be able to login using either username/password combination OR OAuth2 through Google, so there are both “sessions#create” and “sessions#create_with_google” routes.

 Also I setting up partials to use local variables allows you to use the partials across any controller view without needing to duplicate the code.
I created methods in helpers folder, models folder, html in views folder, tables  and data in db folder, routes and omniauth.rb file in config folder, in addition I created .env folder to write google client id & secret.

This project was really fun and challeging to build. I learned a lot and still I feel I’ve to learn more in Rails. 

# Code & Demo
You can check out this project on Github 'https://github.com/Gebre2020/vacation-rails-project' or see the demo 'https://www.youtube.com/watch?v=AuyppfWgn9E' hosted.

## License & copyright
Licensed under the [MIT License](LICENCE).