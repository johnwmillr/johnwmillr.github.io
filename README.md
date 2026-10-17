[My website.](http://www.johnwmillr.com/)

Based on [Kopplin's](https://github.com/sergiokopplin) excellent [Indigo theme](https://github.com/sergiokopplin/indigo).

## Local development

```sh
# Light theme
bundle exec jekyll serve --config _config.yml,_config-dev.yml

# Dark theme
bundle exec jekyll serve --config _config.yml,_config-dev.yml,_config-dark.yml
```

Set `dark-theme: true` in `_config.yml` to publish the dark theme.
