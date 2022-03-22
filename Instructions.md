## Our Second Rails Creation



1. Make sure docker is running
2. Open a terminal and navigate the directory on your computer containing this repository. 
3. If you are on an M1 Mac uncomment the line `platform: linux/amd64` in the `docker-compose.yml` file.
4. Create a new directory in the working directory named `mysql_data`.  This is where the database files will be stored.
5. `docker-compose build` build our docker image
6. `docker-compose up -d` start our docker image
7. `docker-compose run app rails new . --force --database=mysql` generate all the base rails application files.
8. replaced the `config/database.yml` with `SavedFiles/database.yml`
9. Install the new rails gems buy running `docker-compose run app bundle install`
10. `docker-compose run app bin/rails db:create` to create the database
11. `docker exec -it cs351Rails2 bash` enter the docker image 
12. Create a new Homepage and Why travel with us page:
    1. `rails generate controller welcome index why` will create a welcome controller with 2 methods index and about, as well as the views to go with them. 
    2. Open the `config/routes.rb` file to see two new routes have been added `get 'welcome/index'` and `get 'welcome/why'`
    3. In a browser open `http://localhost:3001/welcome/index` to see the index page. `
    4. Let's make it the index by adding the line `root "welcome#index"` to the routes.rb file.
    5. replace the file `app/views/welcome/index.html.erb` with `SavedFiles/welcome/index.html.erb`
    6. View the updated homepage `http://localhost:3001`
    7. Copy the `home-page-banner.jpg` from SavedFiles to `app/assets/images/`
    8. Edit `app/views/welcome/inaex.html.erb` by replacing the line `<img src="images/home-page-banner.jpg" alt="" title="Acme Adventure Travel" width="100%">` with `<%= image_tag 'home-page-banner.jpg', alt:"Family on a river raft", title:"Acme Adventure Travel", width:"100%" %>` This is a helper function that allows you to display images from the assests folder. 
    9. View the homepage again to see the fixed image.
    10. View the page source to see that the image file path contains a long sring of numbers.  This path will change everytime the image is updated to prevent the browswers from caching an outdated image file. 
13. Updating the layout
    1. Replace the `app/views/layouts/applaction.html.erb`  layout template with the `SavedFiles/application.html.erb`. This layout will be the default layout for all pages unless otherwise specified. 
    2. Copy the `SavedFiels/logo-horizontal.png` into `app/assets/images/` 
    3. View the homepage.
13 Making the why travel with us page:
    4. Create a reasons resource by typing `rails generate scaffold Reason title:string content:text` to generate all the files for our reasons resource.  
    5. Note that routes, views, migration, model and controller have all been added for the Reasons have been added. 
    6. Update the database by running the migration by typing `rails db:migrate`
    7. Go to `http://localhost:3001/reasons` in your browswer and enter a few reasons using the scaffolding. You can copy them from the homework if you'd like. 
    8. Next edit the `app/controllers/welcome_controller.rb` file by added the line `` to the why method. This will grab all the Reasons from the reasons table in the database so we can display them in on the why travel with us page. 
    9. Update the routes by changing the line `get 'welcome/why'` to `get 'why-travel-with-us' => 'welcome#why'`
    10. View `http://localhost:3001/why-travel-with-us`
    11. Open the `app/views/welcome/why.html.erb`
        1. Update the h1 to read "Why Travel with Us" and delete the p tag along with it's content.
        2. Add the following lines 
           ```  
           <% @reasons.each do |reason| %>
              <h2><%= reason.title %></h2>
           <p><%= simple_format reason.content %></p>
           <% end %>
           ```
    12. View the `http://localhost:3001/why-travel-with-us` page. 
    