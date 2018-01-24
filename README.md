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

For now, select only the "Hosting" option and connect it to the Firebase project set up earlier. Change "public" target to point to the "build/es5-bundled" directory but keep other responses as default.

```
? Which Firebase CLI features do you want to setup for this folder? Press Space to select featur
es, then Enter to confirm your choices. Hosting: Configure and deploy Firebase Hosting sites

=== Project Setup

First, let's associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add, 
but for now we'll just set up a default project.

? Select a default Firebase project for this directory: news-app-polymer (news-app-polymer)

=== Hosting Setup

Your public directory is the folder (relative to your project directory) that
will contain Hosting assets to be uploaded with firebase deploy. If you
have a build process for your assets, use your build's output directory.

? What do you want to use as your public directory? build/es5-bundled
? Configure as a single-page app (rewrite all urls to /index.html)? No
✔  Wrote build/es5-bundled/404.html
? File build/es5-bundled/index.html already exists. Overwrite? No
i  Skipping write of build/es5-bundled/index.html
i  Writing configuration info to firebase.json...
i  Writing project information to .firebaserc...

✔  Firebase initialization complete!
```

Now deploy to Firebase.

```
firebase deploy

=== Deploying to 'news-app-polymer'...

i  deploying hosting
i  hosting: preparing build/es5-bundled directory for upload...
✔  hosting: 138 files uploaded successfully

✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/news-app-polymer/overview
Hosting URL: https://news-app-polymer.firebaseapp.com
```

Vist the site to make sure the app is deployed correctly.

## 4. Explore the Architecture

This is full-featured Progressive Web App generated using the [Polymer App Toolbox](https://www.polymer-project.org/2.0/toolbox/). This means it has the following capabilities out-of-the-box:
 * Component-based architecture
 * Using web components (and Polymer)
 * Responsive design (using [app-layout elements](https://www.webcomponents.org/element/PolymerElements/app-layout))
 * Modular routing (using [app-route elements](https://www.webcomponents.org/element/PolymerElements/app-route))
 * Localization (with [app-localize elements](https://www.webcomponents.org/element/PolymerElements/app-localize-behavior))
 * Turnkey support for local storage (with [app-storage elements](https://www.webcomponents.org/element/PolymerElements/app-storage) which can include both indexeddb and firebase options)
 * Offline caching as a progressive enhancement using service workers
 * Build tooling to support both unbundled app delivery (HTTP/2) and bundled delivery (HTTP/1)

Features are additive. You can start with simple responsive design layout, then start adding in other pieces as you go (e.g., routing, localization) to get better support.

This [case study](https://news-docs.polymer-project.org/docs/case-study.html) walks through the key features.

### 4.1 App Structure

### 4.2 Views and Routing

### 4.3 Routing and Data Binding

### 4.4 Resource URLs

### 4.5 Displaying Ads

### 4.6 Accelerated Mobile Pages (AMP) [Version](https://github.com/Polymer/news/tree/amp)

### 4.7 [Customization](https://news-docs.polymer-project.org/docs/using.html) and [Theming](https://news-docs.polymer-project.org/docs/theming.html)

