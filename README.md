# rails-base

Starter config for a Dockerized rails API with a postgres db.

Setup:
Make sure to replace "app" in the dockerfile, docker-compose.yml, and entrypoint with the name of the application.
And when database.yml is created by rails new, make sure the db names are correct there as well. (Pass in the app name to `rails new` if you want, otherwise the . syntax below will use the folder name as the app name).

```
docker-compose run --no-deps api rails new . --rc=".railsrc"
```

where api is the name of the api service defined in docker-compose.yml

Then rebuild the image

```
docker-compose build
```

Then change config/database.yml default block to:
```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password
  # For details on connection pooling, see Rails configuration guide
  # http://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
```
And then:
```
docker-compose up
docker-compose run api rake db:create
```

You should now be able to navigate to localhost:8000 and see the welcome to Rails page.

Links:
-https://docs.docker.com/compose/rails/
-https://www.freecodecamp.org/news/painless-rails-development-environment-setup-with-docker/
-https://gist.github.com/eliotsykes/ace0222174804372b51a
