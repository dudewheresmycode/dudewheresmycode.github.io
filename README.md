I mainly followed [this guide](https://ddewaele.github.io/running-jekyll-in-docker/) to get started, but added a docker-compose file so I wouldn't have to remember the longer commands from that guide.


#### Running the blog locally:

```bash
docker-compose up develop
```

This will watch and rebuild on file changes.


Building the static files:

```bash
docker-compose up static
```

This will just generate the static `_site` files.



create a fresh site
```bash
docker run --rm --volume="$PWD/new:/srv/jekyll" -it jekyll/jekyll:3.8 jekyll new .
```

create a fresh theme
```bash
docker run --rm --volume="$PWD/theme:/srv/jekyll" -it jekyll/jekyll:3.8 jekyll new-theme .
```