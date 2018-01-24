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

This creates multiple builds. For our firebase deployment we want to target just one -- we'll target _es5-bundled_.

## 1. Create Firebase Project

As usual, go to Firebase Console and set up a new project (e.g., I used _news-appp-polymer_) to become your backend for this app.

## 2. Build the Polymer Project

Let's check that our project CAN build locally, then verify the build. See the original project's [README](https://github.com/Polymer/news) for directions.

```
$ cd news-app
$ bower install
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/news/
```

Open the browser to ```http://127.0.0.1:8081``` and verify your app is running locally. 

Then build the optimized (bundled) versions for deployment, and verify that *those* work. Use ```polymer serve`` with the specific build preset that you plan to deploy e.g., we'll target build/es5-bundled

```
$ polymer build
$ polymer serve build/es5-bundled
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/es5-bundled/

```

## 3. Deploy to Firebase Hosting

At this point we are NOT using Firebase APIs. Rather, we are just setting up the project for deployment using the Firebase Hosting capability. This puts the News App on a server with HTTPS and CDN support (making it secure and scalable for use) with built-in versioning control (for easy rollback to previous deployments on error)

First install [Firebase CLI](https://github.com/firebase/firebase-tools) if you don't have it
```
npm install -g firebase-tools
```

Then initialize your project:
```
cd news-app
firebase init
```