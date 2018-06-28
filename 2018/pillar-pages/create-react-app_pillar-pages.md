# Quick React Apps with `create-react-app`

The [`create-react-app`](https://github.com/facebook/create-react-app) library from the Facebook team helps you build up React applications with no build configurations. There is definitely a lot you can learn from building your React apps from the ground up but once you feel comfortable `create-react-app` takes care of the tedious work for you. Not to discourage beginners from using this scaffolding tool, just know there is a lot going on under the hood. You can learn a lot from breaking a project built with `create-react-app` too ;). Okay, let's dig in.

## Building a Project 
To start with a fresh project is as simple as running three lines of code in your terminal. Then you're all set with a simple React app.

```bash
npx create-react-app cool-new-app
cd cool-new-app
npm start
```

*[npx](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) is a tool offered in npm@5.2.0 that installs a temporary package and calls it*

You can also install `create-react-app` globally to use at your leisure. Once you create a project this is what the project's file structure will look like:

```
my-app
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── registerServiceWorker.js
```

When you run `npm start` or `yarn start` you can then preview your project at `http://localhost:3000`. As you make changes to your app the page will reload when you save. You will also be able to see build errors and lint warnings in your console where you launched the app.

## But Wait There's More!

There are many other goodies you get with `create-react-app` like [testing](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#running-tests) and a `build` script. Although setup is as simple as those three lines of code there is a lot to it, so check out the handy [User Guide](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.

One of my favorite extras are the two files that give you Progressive Web App support. For those not familiar with PWAs they are basically a way to use modern web technologies like a Web App Manifest, Service Worker API and Push API to help make your web apps more accessible, reliable and engaging. You can read more information by checking out this [blog series](https://www.telerik.com/blogs/a-gentle-and-practical-introduction-to-progressive-web-apps) from Raymond Camden.

When you use `create-react-app` you get two PWA pieces:
- the `manifest.json` file in the `public` directory
- a Service Worker file, `registerServiceWorker.js` in the `src` directory

The `manifest.json` file gives the browser information on how to display your application. This includes things like `"display": "standalone"` which tells the browser to show the app fullscreen by removing the browser chrome. It also sets you up to add a `short_name` and `icons` to control how your app is displayed on a user's device if they opt to install your application. Here is what the default `manifest.json` file looks like:

```json
{
  "short_name": "React App",
  "name": "Create React App Sample",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x16",
      "type": "image/x-icon"
    }
  ],
  "start_url": "./index.html",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}
```

`create-react-app` takes advantage of the [`sw-precache-webpack-plugin`](https://github.com/goldhand/sw-precache-webpack-plugin) in the production configuration of your project. This works to create a service worker file that will automatically cache all your local assets. It will aso keep them up-to-date when you deploy updates. So, with this service worker if someone tries to access your app with a slow or even no connection to their network, the cached resources will be served. One thing to note, on the very first visit to your app the service will need to be registered before serving cached resources. So, only on the n+1 visit will the service worker be ready to use what you have cached.

There are many ways to use or even disable these PWA resources. I highly suggest checking out the [Making a Progressive Web App](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#making-a-progressive-web-app) section in the `create-react-app` docs. There is also a lot that you can do with service workers, like push notifications, and many things you can break. With that in mind it's a great idea to do some [service worker research](https://developers.google.com/web/showcase/2015/service-workers-iowa) and [heed any service worker advice from the experts](https://www.crowdcast.io/e/dshawaf4/register?utm_source=profile&utm_medium=profile_web&utm_campaign=profile).

With all this in mind `create-react-app` is a great tool to help spin up React apps quickly and gives you lots of additions to work with. It is a great resource for those building their 1,000th React app and possibly a good starting place for developers new to React that like to dive in headfirst. Whichever your approach the Facebook team that built `create-react-app` have supplied you with thorough documentation to get you coding.
