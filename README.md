# Jekyll Website Setup

### Docker compose
- `vi docker-compose.yml`
    ```yaml
    version: "3"
    services:
    site:
        command: jekyll serve
        image: jekyll/jekyll:latest
        volumes:
        - $PWD:/srv/jekyll
        - $PWD/vendor/bundle:/usr/local/bundle
        ports:
        - 4000:4000
        - 35729:35729
        - 3000:3000
        -   80:4000
    ```

## Creating a new site
```console
sudo -E docker-compose run site jekyll new site
```

## Developing
```console
sudo -E docker-compose run site bundle update
sudo -E docker-compose run site jekyll b
sudo -E docker-compose run --service-ports site jekyll serve --source site
```
