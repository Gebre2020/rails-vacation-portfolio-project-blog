# rails-vacation-portfolio-project-blog
 
  My third Flatiron project assignment was to build a rails app from scratch.
  My app is called, vacation-rails-project.
  
  - The requirements to complete the rails project are as follows. 
    1. Use the Ruby on Rails Framework.
    2. Models must include at least one has_many, at least on belongst_to, and at least two has_many :through    relationships. Include a many-to-many relationship implemented with has_many :through associaties. Join table must include a user-submittable attribute.
    3. Models must include reasonable validations for simple attributes.
    4. Must include at least one class level ActiveRecord scope method, and it must be chainable.
    5. Must provide standard user authentication, including signup, login, logout, and passwords.
    6. Must also allow login from some other service, Facebook, Twitter, etc.
    7. Must include and make use of a nested resource with the appropriate RESTful URLs. Must include a nested new route with form that relates to the parents resource. Must include a nested index or show route.
    8. Forms should corrently display validation errors. Error messages describing the validation failures must be present within the view.
    9. Application must be, within reason, DRY!
    10. Do not use scaffolding to build the project.

    Models
      First I created the relationships between the model class. Then I run 'rails new vacation-rails-project' in my terminal. Using the resources generator I run user, location, trip, & travel.

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

    I also added validations to the group model to validate the group name, and I checked the relationships with running rails console.
    In the models I created the scope methods, reasonable validations,  user authentication, including signup, login, logout, and passwords, login from google service. Also I make a nested resource with the appropriate RESTful URLs with a nested new index or show routes with form that relates to the parents resource. I make the form to display validation errors messages describing the validation failures within the view. I make the application 'DRY' by using layouts, partials, helpers and refactoring.

    Controllers
    There are five (locations, sessions,travels, trips, and users) controllers. The controllers implement RESTful routes and more importantly nested routes.
    Also I created methods in helpers folder, models folder, html in views folder, tables  and data in db folder, routes and omniauth.rb file in config folder, in addition I created .env folder to write google client id & secret.

    This project was really fun and challeging to build. I learned a lot and still I feel I’ve to learn more in Rails.

