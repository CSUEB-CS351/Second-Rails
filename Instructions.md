## Our Second Rails Creation

We'll be loosely follow the introduction to Rails video from the rubyonrails.org's homepage.  This way if you wish to got back and review you can watch his video and follow loosely along.  I've simplified his example, and modified it to work within a docker environment. 

1. Make sure docker is running
2. Open a terminal and navigate the directory on your computer containing this repository. 
3. If you are on an M1 Mac uncomment the line `platform: linux/amd64` in the `docker-compose.yml` file.
4. Create a new directory in the working directory named `mysql_data`.  This is where the database files will be stored.
5. `docker-compose build` build our docker image
6. `docker-compose up -d` start our docker image
7. `docker-compose run app rails new . --force --database=mysql` generate all the base rails application files.
8. replaced the `config/database.yml` with `SavedFiles/database.yml`
9. `docker-compose run app bin/rails db:create` to create the database
10. `docker exec -it cs351Rails bash` enter the docker image 
11. Create a new Homepage and About Us page:
    1. `rails generate controller welcome index about` will create a welcome controller with 2 methods index and about, as well as the views to go with them. 
    2. Open the `config/routes.rb` file to see two new routes have been added `get 'welcome/index'` and `get 'welcome/about'`
    3. In a browser open `http://localhost:3001/welcome/index` to see the index page. `
    4. Let's make it the index by adding the line `root "welcome#index"` to the routes.rb file.