# [Using the News App](https://news-docs.polymer-project.org/docs/using.html)
Building, using &amp; extending the Polymer 2.0 News App Case Study. See https://news-docs.polymer-project.org/docs/using.html

You can [see the original News App Demo here](https://news.polymer-project.org/)

## 0. Download Code

I elected to [download the repo as a zipfile](https://github.com/Polymer/news) and unzipped it in the root directory. It created a _news-master_ subdirectory, which I renamed to _news-app_.

```
$ cd news-app
$ bower install
$ polymer serve
```

The default polymer.json build configuration is as follows:

```
{
  "entrypoint": "index.html",
  "shell": "src/news-app.html",
  "fragments": [
    "src/news-list.html",
    "src/news-article.html",
    "src/news-path-warning.html",
    "src/lazy-resources.html"
  ],
  "sources": [
    "src/**/*",
    "images/**/*",
    "data/**/*"
  ],
  "extraDependencies": [
    "manifest.json",
    "bower_components/webcomponentsjs/*"
  ],
  "lint": {
    "rules": ["polymer-2-hybrid"]
  },
  "builds": [
    {
      "preset": "es5-bundled"
    },
    {
      "preset": "es6-unbundled"
    },
    {
      "preset": "es6-bundled"
    }
  ]
}
```

This creates multiple builds. For our firebase deployment we want to target just one -- we'll target _es6-bundled_.


