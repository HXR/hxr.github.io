# Jekyll Website Setup

```console
cd docs
sudo -E docker run --rm --volume=$PWD:/srv/jekyll -p 35729:35729 -p 4000:4000 -it jekyll/builder:latest jekyll build
```

## Layout
```
.
├── docs            # Where the site is kept
│   ├── _config.yml # Jekyll config
│   ├── assets      # Images and other media
│   ├── contact.md  # contact webapge
│   ├── css         # static style sheets
│   ├── _includes   # html templates
│   ├── index.md    # index page
│   ├── js          # js
│   ├── _layouts    # jekyll templates
│   ├── _site       # build of the site, in .gitignore
│   └── vendor      # vendor files
├── _site           # build of the site, in .gitignore
└── vendor          # vendor files
```

## Developing
```console
sudo -E docker-compose run site bundle update
sudo -E docker-compose run site jekyll build
sudo -E docker-compose run --service-ports site jekyll serve --source docs
```

## Docker compose
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
sudo -E docker-compose run site jekyll new docs --blank
```

