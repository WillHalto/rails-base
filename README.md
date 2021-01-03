# rails-base

Starter config for a rails API with Docker.

Setup:
Make sure to replace "app" in the dockerfile with the name of the application
And when database.yml is created by rails new, make sure the db names are correct there as well. (Pass in the app name to `rails new` if you want, otherwise the . syntax below will use the folder name as the app name).

```
docker-compose run --no-deps api rails new . --rc=".railsrc"
```

where api is the name of the api service defined in docker-compose.yml

Then rebuild the image

```
docker-compose build
```

Then create the database

```
docker-compose run api rake db:create
```

Then run with

```
docker-compose up
```

Links:
https://docs.docker.com/compose/rails/
https://www.freecodecamp.org/news/painless-rails-development-environment-setup-with-docker/
https://gist.github.com/eliotsykes/ace0222174804372b51a
