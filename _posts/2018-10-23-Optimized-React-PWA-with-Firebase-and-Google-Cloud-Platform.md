---
lang: en
title: Optimized React PWA with Firebase and Google Cloud Platform
description: A boilerplate made for PWA development with React and Firebase deploy.
date: '2018-10-23T12:18:35.783Z'
categories:
  - boilerplates
keywords:
  - react
  - webpack
  - google-cloud-platform
  - firestore
  - material-ui
---

![](img/0__gLaP4yAbKEXvmBZi.jpg)

These last days I’ve been experimenting a little with PWA and React in a [personal repo](https://github.com/nahuelhds/react-pwa-guide-app-v2) based on the React PWA Guide from [codebusking](https://github.com/codebusking/react-pwa-guide-app).

You can use my repo as a PWA boilerplate in order to jump directly to code with React without worrying in the details.

<!-- markdownlint-disable MD033 -->
<div class="github-card" data-github="nahuelhds/react-pwa-guide-app-v2" data-width="100%" data-height="auto" data-theme="default"></div>
<script src="//cdn.jsdelivr.net/github-cards/latest/widget.js"></script>
<!-- markdownlint-enable MD033 -->

### Features

*   **Material Design and AppShell:** Responsive, fit any form factor, desktop but the first is mobile. AppShell architecture implemented wearing material design got bressed by [material-ui.com](https://material-ui.com/)
*   **ES6 via Babel:** You can use ES6 feature with same babel-preset to [create-react-app](https://github.com/facebookincubator/create-react-app) and dynamic module importing
*   **Webpack — Remarkable configurations:** Webpack configuration file has been written in configurable, optimzied and easy settings
*   **Webpack — Developing Progressive Web App:** You can check them of optimized bundling for PWA including code-splitting, multiple chunk and [preload](https://www.npmjs.com/package/preload-webpack-plugin). As developing, reloading changes instantly by webpack-dev-server, also it is working well with [service worker](https://github.com/ragingwind/sw-precache-webpack-dev-plugin)
*   **HTTPS:** Deploying to Firebase Hosting to run perfectly on HTTPS with PWA features
*   **Web Push:** Web Push demo also is branded at this app by Firebase Push Messaging
*   **Service Worker:** Generating service worker scripts is completly intergrated in build process with Webpack 2 and plugins
*   **Web Manifest:** Have a look how to installable webapp work by Web Manifest
*   **Realtime Database:** integrated firebase to show PWA how to work with fetched data and cached data via service worker
*   **Code splitting:** for speed optimization and initial page fast load.
*   **React Lite Support:** To achieve minimal vundle size at initializing time of the app, we support for building with react-lite. Simple, you can get another version of app running on `react-lite` if you could add the additional argument on build command when you build `-- --env.lite`

### My updates and additions

*   **Updated** Webpack 4 and all the plugins used in the config.
*   **Updated** to Babel 7
*   **Added** [React Hot Loader](https://github.com/gaearon/react-hot-loader) for realtime coding experience
*   **Updated** to React 16.5 & PropTypes
*   **Removed** React Tap Event Plugin as it is deprecated since React 16.4. See [https://github.com/zilverline/react-tap-event-plugin](https://github.com/zilverline/react-tap-event-plugin)
*   **Added** [Loadable Component](https://github.com/smooth-code/loadable-components) for code splitting and in replacement of the `asyncComponent` method.
*   **Updated** to Material UI 3.3.0
*   **Updated** to Firebase 5.5.4
*   **Added** [Cloud Firestore](https://firebase.google.com/docs/firestore/?hl=es-419) for the database implementation in the _Users_ component.

Happy coding!
