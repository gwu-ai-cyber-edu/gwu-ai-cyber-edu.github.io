# AI in Cybersecurity Education

This directory contains the Jekyll site for the AI in Cybersecurity Education summer institute.

## What is here

- `index.md`: the site homepage that GitHub Pages renders.
- `schedule.md`: the schedule page linked from the top navigation.
- `_layouts/default.html`: the local page layout used for both pages.
- `assets/css/style.scss`: site styling, including the header nav and table/button rules.
- `_config.yml`: Jekyll and theme configuration.
- `.github/workflows/jekyll-gh-pages.yml`: GitHub Pages build and deploy workflow.

## Install

Use Ruby 4 locally, then install the bundle from this directory:

```sh
bundle install
```

## Local Development

Start the site with:

```sh
bundle exec jekyll serve
```

If Bundler picks up stale gems from a previous Ruby version, rebuild the local bundle:

```sh
rm -rf vendor/bundle
bundle install
bundle exec jekyll serve
```

## GitHub Pages

The repository is configured to build with the GitHub Pages workflow in `.github/workflows/jekyll-gh-pages.yml`. The site uses `jekyll-theme-minimal` and standard Jekyll pages, so it should continue to render on GitHub Pages without the old `remote_theme` setup.
