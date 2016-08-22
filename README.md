# c9_recipe
Recipe for creating new ruby app using cloud9

1. pray to Charles Babbage and Steve Jobs for guidance 
   
2. cloud9 (c9)
  - create new workspace
  - choose blank template

3. c9 (terminal)
  -Create a gemset for Rails 4.2.5:
    $ rvm gemset create rails425

  - Switch to the rails425 gemset:
    $ rvm @rails425
    $ rvm current

  - Install Rails 4.2:
    $ gem install rails -v 4.2.5

4. create new Rails app (c9)
    $ rails new app_name -T
    - The -T option specifies that the app should not be created with standard test packages since we'll be testing our app with RSpec.

5. Replace the contents of your Gemfile with the following:

Gemfile
 source 'https://rubygems.org'
 
 # Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
 gem 'rails', '4.2.5'
 
 group :production do
   gem 'pg'
   gem 'rails_12factor'
 end
 
 group :development do
   gem 'sqlite3'
 end
 
 gem 'sass-rails', '~> 5.0'
 gem 'uglifier', '>= 1.3.0'
 gem 'coffee-rails', '~> 4.1.0'
 gem 'jquery-rails'
 gem 'turbolinks'
 gem 'bootstrap'
 gem 'figaro'
 gem 'pry'

 group :development, :test do
   gem 'byebug'
   gem 'web-console', '~> 2.0'
   gem 'spring'
   gem 'rspec-rails'
   gem 'shoulda'
   gem 'faker'
   gem 'factory_girl_rails'
 end
  
6. Update our application with bundle install --without production. This command installs everything specified in the Gemfile and ensures that all of the gems work harmoniously. The --without production option ignores gems in group :production. These gems aren't needed or used in our Development environment. Our Production environment will automatically run bundle install when we deploy, and will account for gems declared in group :production at that point.
  
  $ bundle install --without production

7. Run the following command in your terminal to create the database
  $ rake db:create

8. Heroku Gemfile additions (minor configuration changes to properly serve assets on Heroku)
  Gemfile
 ...
 group :production do
   gem 'pg'
   gem 'rails_12factor'
 end

 group :development do
   gem 'sqlite3'
 end
 ...

$ bundle install

9. Test Locally to make sure app is working:
  $ rails s -p $PORT -b $IP

10. Git and Github
  - Sign into GitHub account and create a new repo named "app_name". You've already created a README, so make sure the "Initialize this repository with a README" is unchecked.

11. c9 - push app code to Git
  $ git init
  $ git add .
  $ git commit -m 'First commit and README update'
  $ git remote add origin git@github.com:<user name>/<repo_name>.git
  $ git push -u origin master  

  - reolad GitHub homepage to verify repo was updated

12. Deploying to Heroku
  $ heroku login
    - after logging in...
  $ heroku create
    - create new app
  $ git push heroku master
    - push code from master branch of Git repo to Heroku
    -  If you receive an error that says Permission denied (publickey)
        - https://devcenter.heroku.com/articles/keys#adding-keys-to-heroku
  $ heroku apps:info
    - see web address for app

*****************************************************************************************************************************
https://www.bloc.io/resources/getting-started-with-rails-web-development-projects

13. Generating a Controller and Views
  $ rails generate controller welcome index about
    -  The first argument represents the controller name, which is welcome. The next two arguments (index and about) represent views corresponding with the welcome controller. 
  $ rails s -p $PORT -b $IP
    test app to make sure pages are showing
      /welcome/about
      /welcome/index

14. Routing
  config/routes.rb
+ root 'welcome@index'
  - The root method allows us to declare the default page the app loads when we navigate to the home page URL. Test it by going to localhost:3000. You should see the welcome index view by default.

$ rake routes
  - View your app's available routes by typing rake routes from the command line. 

15. HTML and CSS
add:  
- app/views/layouts/application.html.erb
   <body>
   <ul>
      <li><%= link_to "Home", welcome_index_path %></li>
      <li><%= link_to "About", welcome_about_path %></li>
   </ul>

   <%= yield %>

 </body>

add:

app/assets/stylesheets/welcome.scss
   h1 {
   color: red;
    }














