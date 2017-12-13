# JavaScript's Journey Through 2017

Another year has gone by and JavaScript is still going strong. Probably not a surprise to any of us but may be to the demise of some. Hopefully, options overload and the complexity of coding in JavaScript has not made anyone throw their computer out the window. In reviewing JavaScript in the past year there are a few topics that stand out that I'll be covering:

- ECMAScript Goodies
- How to JavaScript in 2017
- Package Manager Rumble
- PWAs: The JavaScript Overview

There are may be other things I could cover, if you think of any, add a comment, let's discuss! Okay, here we go.

![deep breath](images/deep-breath.gif)

*deep breath in*

## ECMAScript Goodies

Let's check in with [Ecma International, Technical Committee 39](https://github.com/tc39)! It turns out the 6 in ES6 does not stand for the number of years it takes for a release. I kid! Since ES6/ES2015 took so long to release (6 years, hence my jab) that the moved to a yearly small-batch release instead. I'm a big fan of this and I think the momentum keeps things moving and JavaScript improving. What presents did we get for ES2017 and what's on our list for ES2018?

### ES2017
In January at the TC39 meeting the group settles on the ECMAScript proposals that would be slated as the features of ES2017 (also referred to ES8, which probably should be nixed to avoid confusion). This list includes:

**Major features**
-	Async Functions 
-	Shared Memory and Atomics

**Minor features**
-	`Object.values/Object.entries`
-	String padding
-	`Object.getOwnPropertyDescriptors()`
- Trailing commas in function parameter lists and calls

### Async/Await

I'm starting here because of the alphabet and my level of excitement is pretty high for this nifty addition. In ES6 we got [`promises`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) to help us with the all too familiar condition commonly known as...
![ugh do i have to say it?](images/say-it.gif)

CALLBACK HELL 😱.

- (Brian Terlson) https://github.com/tc39/ecmascript-asyncawait
- a syntax that reads entirely synchronously insipired by TJ Holowaychuk's [Co](https://github.com/tj/co) package.
- As a quick overview, `async` and `await` keywords allow you to use them and `try/catch` blocks to make functions behave asynchronously. They work like generators but are not translated to Generator Functions. This is what that looks like:

```js
// Old Promise Town
function fetchThePuppies(puppy)
  return fetch(puppy)
    .then(puppyInfo => puppyInfo.text())
    .then(text => {
      return JSON.parse(text)
    })
    .catch(err => {{
      console.log(`Error: ${err.message}`)
    })
}
```

```js
// New Async/Await City
async function fetchThePuppies(puppy)
  try {
    let puppyInfo = await fetch(puppy)
    let text = await puppyInfo.text()
    return JSON.parse(text)
  }
  catch (err) {
    console.log(`Error: ${err.message}`)
  }
}
```

### Shared Memory and Atomics
Wait, did we enter a theoretical physics class? Sounds fun, but no. This ECMAScript propsal joined the ES2017 line up and introduces `SharedArrayBuffer` and a namespace object `Atomics` with helper functions. We'll dive in a little but for a more detailed look: [Dr.Axel to the rescue!](http://2ality.com/2017/01/shared-array-buffer.html) 

-`SharedArrayBuffer`
- `Atomics`
- Lars T. Hansen https://github.com/tc39/ecmascript_sharedmem

### `Object.values/Object.entries`
- Jordan Harband https://github.com/tc39/proposal-object-values-entries
- Getting the actual values of each entry
- `entries`
- compared to iterators

### String Padding
I didn't think I was going to have to say this again but, left pad. Yes, the [left pad](http://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm) debacle of 2016 raised the attention of the JavaScript community enough for TC39 to add string padding.

- (Jordan Harband, Rick Waldron) https://github.com/tc39/proposal-string-pad-start-en
- padStart/padEnd
- trimRight/trimLeft

### `Object.getOwnPropertyDescriptors()`
-	(Jordan Harband, Andrea Giammarchi) https://github.com/tc39/proposal-object-getownpropertydescriptors
- "For each own (non-inherited) property of obj, it adds a property to result whose key is the same and whose value is the former property’s descriptor."

### Appreciation Pause
Now, there are a lot of great people that are and have been on TC39, I would like to thank them all for their work. Doing this list has also put someone’s name literally in writing multiple times: [Jordan Harband](https://twitter.com/ljharb). So, I just wanted to take a quick pause to 👏👏👏👏 Jordan, who is currently on a solid [1,325 day GitHub contributions streak](https://github.com/ljharb) as of December 1, 2017. Thanks for all you do for JavaScript, Jordan!!


### Trailing Commas

- Jeff Morrison
 
I must admit, I think trailing commas looks super sloppy and have never been a big fan.

```js
let why = [
  "really?",
  "must you?",
  "yuck 😝",
]
```

![yuck](images/yuck.gif)

That being said, I get it. I have had many occasions where I add an item to an array, a key value pair to an object, or deleted an item and have had to remove or add a comma. I am one with the concept of saving how many keystrokes you must use. [keysleft.com](http://keysleft.com/) says I only have 213,407,968 and I just blew through 117 in this sentence alone!

### What's to Come in 2018

There is an awesome, emoji-laden table of proposals and what stages they are in located [here](https://github.com/tc39/proposals). You can also see the [finished proposals](https://github.com/tc39/proposals/blob/master/finished-proposals.md) including [one](https://github.com/tc39/proposal-template-literal-revision) that is already ready for 2018 publication!

## How to JavaScript in 2017
Last year many people, including myslef, were talking about JavaScript fatigue. Yes, the ways to write a JavaScript application have not really slimmed down BUT with a lot of CLI tools doing much of the heavy lifting, we can relax a little. 

### CLI Tools
Most all libraries have CLI tools, so what all are they helping us do in 2017?

### Bye Bye Babel?

### TypeScript Talk
If we're talking about how to JavaScript we must talk about TypeScript. TypeScript came out of the Microsoft office five years ago but has been the cool kid in town 😎 in 2017.

For everyone who wanted types in JavaScript, TypeScript is here to offer a strict syntactical superset of JavaScript which gives optional static typing. Pretty cool, if you're into that kind of thing. 

![do your thang](images/your-thang.gif)

> Speaking as someone who proposed types for JavaScript in 2014: I do not believe types are in the cards for the near future. This is an extremely complex problem to get right from a standards perspective. Just adopting TypeScript as the standard would of course be great for TypeScript users, but there are other typed JS supersets with pretty significant usage including closure compiler and flow. These tools all behave differently and it’s not even clear that there’s a common subset to work from (I don’t think there is in any appreciable sense). I’m not entirely sure what a standard for types looks like, and I and others will continue to investigate this as it could be very beneficial, but don’t expect anything near term

- https://twitter.com/mgechev/status/940131449025347589
![typescript and flow benefits](images/typescript-flow.png)

-[HashNode AMA with Brian Terlson](https://hashnode.com/ama/with-brian-terlson-cj6vu9vjv01nmo1wu8vmtt1x9#cj6vuspfq01oso1wuhjo5zvd6) 

- Angular and TypeScript

## Package Manager Rumble
[Npm](https://github.com/npm/npm), [Yarn](https://github.com/yarnpkg/yarn) and [Bower](https://github.com/bower/bower) are still the leaders of the pack...age management tools but I also wanted to throw [jspm](https://github.com/jspm). With close to two million installs this year, jspm still going strong. Now this isn't going to be a package manager brawl, despite the heading of this section, I'll give you the info and you can decide what it means to you 😘 I'm not going to lie though, I use npm and like their team and what they do a ton. So, if I come across as bias, it's probably because I am.

![what can i say](images/bias.gif)


### The Digits
Let's first take a look at the comparative installs for the year. There seems to be an almost even exponential growth between each of these package managers. npm still has a large lead over yarn but is less than double the installs of Bower.

npm - 42,882, 473
bower - 26,929,956
yarn - 11,154,271
jspm - 1,859,116 

[graphed comparison](images/bower-jpsm-npm-yarn.png)
https://npm-stat.com/

### NPM
It's pretty clear to see that there were many aspects of Yarn that users liked: speed, the lockfile...
In response npm released version 5, which was packed with fun things. One of the main focuses of this release was increasing their speed, which, of course, prompted amazing blogpost titles like, ["npm@5 — Yarn killer?"](https://medium.com/netscape/npm-5-yarn-killer-ba69737b24d0) by Nikhil John.

- package.lock
-npx
- `--save` default

There are more features on version 5 in particular, you can check out their [blog](http://blog.npmjs.org/post/161081169345/v500) for more information.


npm 5 updates, speed tests, npx

### Yarn

Even with the updates in npm 5, Yarn is still faster. Oh, you want to see the speed comparison updated on the daily? Well, Thomas Schaaf has just the thing. That's right, [here](https://docs.google.com/spreadsheets/d/1ZE5B4qJw1kNGMzjgslcWTuPYrpatzQJXSYMGNOhZ2ys/edit#gid=263077280) he has a Google doc where each day the speed comparison is updated.

![npm v yarn speed comparison](images/speed.png)
https://github.com/thomaschaaf/npm-vs-yarn 

### Bower

Bower is still the most popular front-end specific package manager BUT while it is still being maintained Bower recommending users switch to using Yarn and Webpack. In October of this year Adam Stankiewicz, made a [post on the Bower blog](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) on how to migrate *off* of Bower pointing to his repo, [bower-away](https://github.com/sheerun/bower-away) that he had created in July. Yet, this years install numbers show Bower with over double the amount of installs of Yarn, so we'll see how that goes 🤔 If you feel like cozing up for a long read, check out this [closed issue](https://github.com/bower/bower/issues/2298) discussing whether or not to deprecate Bower.

![popcorn time](images/popcorn.gif)

### jspm

In their words "jspm is a package manager for the SystemJS universal module loader, built on top of the dynamic ES6 module loader." jspm does not seem to have much GitHub love in the form of forks and stars but there is consistent activity throughout this year.

### The Other Ones

Okay, chunking these all together may seem harsh but, let's be honest, people aren't using them as much as npm, Bower, Yarn or jspm.

Which other ones you may ask? Today we’re going to look at three that are currently doing the best in installs this year: [component](https://github.com/componentjs/component), [pnpm](https://github.com/pnpm/pnpm) and [ied](https://github.com/alexanderGugel/ied). If we take a look at the charts, provided by [npm stats](https://npm-stat.com/) (yes, just like yarn, these can all be installed using npm), pnpm is towering over the other two. I also wanted to show with a chart looking at monthly downloads starting at February 2015 that it looks as if component and ied have hit their peak and slowly dying down whereas pnpm is on an upward trajectory. Let’s briefly dig into each project.

![2017 installs](images/component-pnpm-ied_2017.png)
![installs of their existence](images/component-pnpm-ied.png)

pnpm - 334,497
component - 35,340
ied - 22,522 

[component](https://github.com/componentjs/component) which is a depracated project that hasn't been commited to in 2 years
[pnpm](https://github.com/pnpm/pnpm)
[ied](https://github.com/alexanderGugel/ied) toutes being "like npm, but faster" had its first commit back in August of 2015. It is specifially for Node, has some killer ASCII art but hasn't had a commit in over a year.

Related: Look at this great [list of package managers](https://github.com/topics/package-manager).

## PWAs: The JavaScript Overview
If you haven't heard about Progressive Web Apps, don't worry, my Nana hasn't either 😋. Okay, actually, she has. I mean, she has *me* as her grandaughter after all and I haven't shut up about Progressive Web Apps since I learned about them at the Chrome Dev Summit in 2016. Like her though, you may have heard of them but not fully understood what they are or why they are getting so much attention. Alex Russel brought a name to the concept of PWA's in his blogpost ['Progressive Web Apps: Escaping Tabs Without Losing Our Soul'](https://infrequently.org/2015/06/progressive-apps-escaping-tabs-without-losing-our-soul/) in mid-2015. Yet, he talked about this concept already existing siting [Paul Kinlan's demo](https://developers.google.com/web/updates/2015/03/increasing-engagement-with-app-install-banners-in-chrome-for-android?hl=en) from Chrome Dev Summit 2014. Alex gives a great description of the Progressive Web App concept that starts with one of my favorite analogies of this technology:

> These apps aren’t packaged and deployed through stores, **they’re just websites that took all the right vitamins**. They keep the web’s ask-when-you-need-it permission model and add in new capabilities like being top-level in your task switcher, on your home screen, and in your notification tray. Users don’t have to make a heavyweight choice up-front and don’t implicitly sign up for something dangerous just by clicking on a link. Sites that want to send you notifications or be on your home screen have to earn that right over time as you use them more and more. They progressively become “apps”.

There is a lot of focus on whether or not PWAs are replacing native mobile applications. One, I believe they are not and two, that is mis-directed attention.

browser manufacturers to treat the JS runtime in a mobile browser same as reg brpwser

## Conclusion

In 2017, ECMAScript continued its small but impactful deliveries, the package manager race continues and, per usual, we've finally brought technologies introduced several years ago into the spotlight (i.e. TypeScript, PWAs, etc.).

There are bound to be many more things to talk about in a year's time but, for now, let's be thankful JavaScript has survived another year without burning everything to the ground 😛
