# Building Button

## Getting Started

If you don't have Jekyll already installed, you will need to install it.

```
$ gem install jekyll
$ gem install kramdown
```

### Running locally

Build and start the Jekyll Server. Adding the `--watch` option updates the generated HTML whenever you make changes.

```
$ jekyll serve --watch
```

Now you can navigate to `localhost:4000` in your browser to see the site.

### Page Animation

If you would like to add a [fade-in-down effect](http://daneden.github.io/animate.css/), you can add `animated: true` to your `_config.yml`.
