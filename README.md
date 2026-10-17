[My website.](http://www.johnwmillr.com/)

Based on [Kopplin's](https://github.com/sergiokopplin) excellent [Indigo theme](https://github.com/sergiokopplin/indigo).

## Local development

```sh
# Follows your OS appearance setting (dark-theme: auto)
bundle exec jekyll serve --config _config.yml,_config-dev.yml

# Force the light or dark theme
bundle exec jekyll serve --config _config.yml,_config-dev.yml,_config-light.yml
bundle exec jekyll serve --config _config.yml,_config-dev.yml,_config-dark.yml
```

In auto mode, you can also flip themes without changing your OS setting via
Chrome DevTools > Rendering > "Emulate CSS media feature prefers-color-scheme".
The `dark-theme` setting in `_config.yml` accepts `auto`, `true`, or `false`.
