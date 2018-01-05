# **JavaScript's Journey Through 2017 and Into 2018**

Another year has gone by and JavaScript is still going strong. This is probably not a surprise to any of us. Hopefully, option overload and the complexity of coding in JavaScript has not made anyone throw their computer out the window. In reviewing JavaScript in the past year, there are a few topics that stand out that I'll be covering:

* ECMAScript Goodies

* How to JavaScript in 2017

* Package Manager Rumble

There are may be other things I could cover, if you think of any, add a comment, let's discuss! Okay, here we go.

![image alt text](image_0.gif)

*deep breath in*

## **ECMAScript Goodies**

Let's check in with [ECMA International, Technical Committee 39](https://github.com/tc39)! It turns out the 6 in ES6 does not stand for the number of years it takes for a release. I kid! Since ES6/ES2015 took so long to release (6 years, hence my jab) the committee decided to move to a yearly small-batch release instead. I'm a big fan of this and I think the momentum keeps things moving and JavaScript improving. What presents did we get for ES2017 and what's on our list for ES2018?

**You can learn more about the TC39 process of proposals **[her*e](http://2ality.com/2015/11/tc39-process.html)

### **ES2017**

In January, at the TC39 meeting, the group settles on the ECMAScript proposals that would be slated as the features of ES2017 (also referred to ES8, which probably should be nixed to avoid confusion). This list included:

Major features

* [Async Functions](https://github.com/tc39/ecmascript-asyncawait)

* [Shared Memory and Atomics](https://github.com/tc39/ecmascript_sharedmem)

Minor features

* [Object.values/Object.entries](https://github.com/tc39/proposal-object-values-entries)

* [String padding](https://github.com/tc39/proposal-string-pad-start-end)

* [Object.getOwnPropertyDescriptors()](https://github.com/tc39/proposal-object-getownpropertydescriptors)

* [Trailing commas in function parameter lists and calls](https://github.com/tc39/proposal-trailing-function-commas)

### **Async/Await**

[Proposed by: Brian Terlson](https://github.com/tc39/ecmascript-asyncawait)

I'm starting here because it was first on the list and my level of excitement is pretty high for this nifty addition. In ES2015 we got [promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) to help us with the all too familiar condition commonly known as...

![image alt text](image_1.gif)

CALLBACK HELL 😱.

The async/await syntax reads entirely synchronously and was inspired by TJ Holowaychuk's [Co](https://github.com/tj/co) package. As a quick overview, async and await keywords allow you to use them and try/catch blocks to make functions behave asynchronously. They work like generators but are not translated to Generator Functions. This is what that looks like:

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

This doesn't mean you should go in and replace all promises in your code with async/await. Just like you didn't go in and replace every function in your code with arrow functions (one hopes), only use this syntax where it works best. I won’t go too into detail here because [there](https://msdn.microsoft.com/en-us/magazine/jj991977.aspx) [are](https://hackernoon.com/6-reasons-why-javascripts-async-await-blows-promises-away-tutorial-c7ec10518dd9) [tons](https://ponyfoo.com/articles/understanding-javascript-async-await) [of](https://javascript.info/async-await) [articles](https://developers.google.com/web/fundamentals/primers/async-functions) [covering](https://blog.risingstack.com/mastering-async-await-in-nodejs/) [async/await](https://codeburst.io/javascript-es-2017-learn-async-await-by-example-48acc58bad65). Check them out (yes, I *did* add a link of a async/await blog post for each of those last words in the previous sentence, you’re welcome 😘).

### **Shared Memory and Atomics**

[Proposed by: Lars T. Hansen](https://github.com/tc39/ecmascript_sharedmem)

Wait, did we enter a theoretical physics class? Sounds fun, but no. This ECMAScript proposal joined the ES2017 line up and introduces SharedArrayBuffer and a namespace object Atomics with helper functions. Super high-level (pun intended), this proposal is our next step towards [high-level parallelism in JavaScript](http://2ality.com/2017/01/shared-array-buffer.html).

We're using JavaScript for more and more operations in the browser relying on Just-in-Time compilers and fast CPUs. Unfortunately, as Lars T. Hansen says in his awesome post, [A Taste of JavaScript’s New Parallel Primitives](https://hacks.mozilla.org/2016/05/a-taste-of-javascripts-new-parallel-primitives/) from May 2016:

But JS JITs are now improving more slowly, and CPU performance improvement has mostly stalled. Instead of faster CPUs, all consumer devices — from desktop systems to smartphones — now have multiple CPUs (really CPU cores), and except at the low end they usually have more than two. A programmer who wants better performance for her program has to start using multiple cores in parallel. That is not a problem for "native" applications, which are all written in multi-threaded programming languages (Java, Swift, C#, and C++), but it is a problem for JS, which has very limited facilities for running on multiple CPUs (web workers, slow message passing, and few ways to avoid data copying).

#### **SharedArrayBuffer**

//TODO: add section about putting shared array buffer behind a flag because of the Intel security design flaw.

This proposal provides us with the building blocks for multi-core computation to research different approaches to implement higher-level parallel constructs in JavaScript. What might those building blocks be? May I introduce you to SharedArrayBuffer. [MDN has](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) a great succinct definition so I'll just plop that in right here:

The SharedArrayBuffer object is used to represent a generic, fixed-length raw binary data buffer, similar to the ArrayBuffer object, but in a way that they can be used to create views on shared memory. Unlike an ArrayBuffer, a SharedArrayBuffer cannot become detached.

I don't know about you but the first time I read that I was like, "wat."

![image alt text](image_2.gif)

Basically, one of the first ways we were able to run tasks in parallel was with web workers. Since the workers ran in their own global environments they were unable to share, by default, until communication between the workers, or between workers and the main thread, evolved. The SharedArrayBuffer object allows you to share bytes of data between multiple workers and the main thread. Plus, unlike its predecessor [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer), the memory represented by SharedArrayBuffer can be referenced from multiple agents (i.e. web workers or the web page's main program) simultaneously. You can do this using [postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Worker/postMessage) to *transfer* the SharedArrayBuffer from one of these agents to the another. Put it all together, and what do you got? Transferring data between multiple workers and the main thread using SharedArrayBuffer so that you can execute multiple tasks at once which == parallelism in JavaScript. But wait, there’s more!

![image alt text](image_3.gif)

#### **Atomics**

Okay, the next stop on this parallel train: Atomics, which is a global variable that has two methods. First, let me present you with the problem the Atomics methods solve. 

When sharing a SharedArrayBuffer betwixt 🎩 agents (as a reminder agents are the web workers or the web page’s main program) each of those agents can read and write to its memory at any time. So, how do you keep this sane and organized, making sure each agent knows to wait for another agent to finish writing their data?

Atomics methods [wake](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics/wake) and [load](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics/load)! Agents will "sleep" in the wait queue while waiting for another agent to finish writing their data, so Atomics.wait is a method that lets them know to wake up. When you need to read the data you use Atomics.load to load data from a certain location. The location is based on the methods two parameters a [TypedArray](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays),  an array-like mechanism for accessing raw binary data (what SharedArrayBuffer is using), and an index to find the position in that TypedArray. There *is* more to it than what we’ve just covered but that’s the gist of it.

For now, Atomics has only these two methods. Eventually, Hansen (our lovely author of this proposal and explainer of parallel things) says, there should be more methods, like store and compareExchange, to truly implement synchronization. Again, we are at the beginning stages of parallelism in JavaScript and this proposal is providing us with the building blocks to get there.

Phew! Although that was quite a lot to think about, that was still a high level overview. So, thank your brain for getting you this deep and check out these fantastic resources to dive in more!

* [Dr.Axel to the rescue!](http://2ality.com/2017/01/shared-array-buffer.html) 

* [A Taste of JavaScript’s New Parallel Primitives](https://hacks.mozilla.org/2016/05/a-taste-of-javascripts-new-parallel-primitives/) from Lars T. Hansen

![image alt text](image_4.gif)

### **Object.values/Object.entries**

[Proposed by: Jordan Harband](https://github.com/tc39/proposal-object-values-entries)

#### **Object.values()**

I have actually [benefited from the useful addition of ](https://github.com/tzmanics/U-Go-Hue-Go-Tutorial/tree/5ff8cd88c38f3ad42f40f43aefbda1007b3e391d#get-the-lights)[Object.values](https://github.com/tzmanics/U-Go-Hue-Go-Tutorial/tree/5ff8cd88c38f3ad42f40f43aefbda1007b3e391d#get-the-lights)[ recently](https://github.com/tzmanics/U-Go-Hue-Go-Tutorial/tree/5ff8cd88c38f3ad42f40f43aefbda1007b3e391d#get-the-lights) when pulling Philips Hue light information from an observable. It allowed me to iterate through my data's values because it returns an array of the object's properties.

// land before `Object.values()`
const lights = {{ id: 1, on: true, color: ‘blue’}, { id: 2, on: false, color: ‘red’ }}
this.lights = Object.keys(data).map(key => data[key])

// the time is now aka WITH `Object.values()`
this.lights = Object.values(data)

// both return 
// [{ id: 1, on: true, color: ‘blue’}, { id: 2, on: false, color: ‘red’ }]

Fancy 💅, right?

#### **Object.entries{}**

This method takes what Object.values() does one step further. Looking at an object, a data structure of key-value pairs, each of those pairs is an entry. When you call Object.entries() it is returning an array containing an array for each of those entries.

Object.entries({ name: 'Toshmagosh', age: 12 })
// [[ "name", “Toshmagosh” ], [ “age”, 12 ]]

It's really quite straight forward, but if you ever want to dive in more, [JavaScript.info](https://javascript.info/keys-values-entries) has a good rundown.

### **String Padding**

[Proposed by : Jordan Harband, Rick Waldron](https://github.com/tc39/proposal-string-pad-start-end)

I didn't think I was going to have to say this again but, left pad. Yes, the [left pad](https://developer.telerik.com/featured/left-pad-indicative-fragile-javascript-ecosystem/) debacle of 2016 raised the attention of the JavaScript community enough for TC39 to add string padding. To be fair though, it was about time for JavaScript to have some native methods to handle Strings. ✨ Welcome [padStart](https://codeburst.io/learn-javascript-es-2017-string-padding-padstart-padend-88e90783e7de)[/padEnd](https://codeburst.io/learn-javascript-es-2017-string-padding-padstart-padend-88e90783e7de) to the family, which currently was just a lonely String.prototype.trim (est. ES5)!

![image alt text](image_5.gif)

You are all smart people so you probably can surmise what each of these methods do. So, I'll just show you some examples instead of using my words.

// padStart adds padding until string reaches provided length
'puppies'.padStart(22)
// "               puppies"

// or provide a filler instead of blank spaces
'nachos'.padStart(11, 'yum')
// "yumyunachos"

// padEnd works the same but adds to the end of the string
'Carlos Santana'.padEnd(30, '*-^')
// "Carlos Santana*-^*-^*-^*-^*-^*"

// Emoji trickiness
'🍞🥞🥚🌭'.padEnd(8)
// "🍞🥞🥚🌭" // no pad? yup, because the length === 8, emoji you so funny

To review this, both methods take an integer parameter that is telling them how long the final length of the string, including the padding, should be. If you pass a number shorter or equal to the original length of the string, nothing will change. Bravo, on wasting your time (just kidding 😁). You can also pass a string and padStart/padEnd will repeatedly add each item of that string to the start or end of the original string until the length matches the passed length parameter. As you can see in my example above, since I wanted a length of 11, padStart added ` ‘yum’ then the ‘yu’ and stopped. [Emoji](https://emojipedia.org/faq/) are very important so I wanted to remind you of their tricky string lengths, more information in [this handy blog post](http://blog.jonnew.com/posts/poo-dot-length-equals-two). 

There are more methods in the pipeline: [trimStart/trimEnd](https://github.com/tc39/proposal-string-left-right-trim) is currently at stage 2 (out of the 4 stages, [here’s the process break down again](http://2ality.com/2015/11/tc39-process.html) 🙂👍). This will let us trim or remove starts and ends of strings. Fun fact: this proposal started out with trimLeft and trimRight but has been updated to trimStart and trimEnd to stay consistent with padStart and padEnd. Yay, consistency! It also helps with any confusion whether a language is read right-to-left or left-to-right. ✅

### **Object.getOwnPropertyDescriptors()**

[Proposed by: Jordan Harband & Andrea Giammarchi](https://github.com/tc39/proposal-object-getownpropertydescriptors)

This is the plural version of [Object.getOwnPropertyDescriptor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor) which returns a descriptor of the property that's directly on an object, i.e. not on its prototype chain.

let popcorn = { action: 'pop', butter: true }
let popcornAction = Object.getOwnPropertyDescriptor(popcorn, 'action')

// popcornAction is {
//   value: "pop",
//   writable: true,
//   enumerable: true,
//   writable: true
// }

So, using the plural version you are able to capture all of an object's non-inherited (or own) property descriptors. Using the delicious example above:

let popcorn = { action: 'pop', butter: true }
let popcornProperties = Object.getOwnPropertyDescriptors(popcorn)

// popcornProperties is {
//   action: {
//     value: "pop",
//     writable: true,
//     enumerable: true,
//     writable: true
//   },
//   butter: {
//     value: true,
//     writable: true,
//     enumerable: true,
//     writable: true
//   }
// }

Why do we need these methods? Well the proposer, Jordan Harband, puts it well here:

There is not a single method in ECMAScript capable of simplifying a proper copy between two objects. In these days more than ever, where functional programming and immutable objects are essential parts of complex applications, every framework or library is implementing its own boilerplate in order to properly copy properties between composed objects or prototypes. — Jordan Harband

With this addition you can now use getPrototypeOf and getOwnPropertyDescriptors with objectCreate to copy object and easily give it the same prototype and property descriptors. Before, this was most often done using Object.assign, which would grab an object's properties and symbols instead of descriptors. That approach left the risk of discarding possible accessors.

// just to give you a bit of an idea
const toshmagosh = {
  cuteLevel: 11,
  breed: 'Blue Pomeranian',
  treatTime: treat => {
    console.log(`Do you want a ${treat}?`)
  }
}

const newPuppy = Object.create(
  Object.getPrototypeOf(toshmagosh),
  Object.getOwnPropertyDescriptors(toshmagosh)
);

// newPuppy
// {cuteLevel: 11, breed: "Blue Pomeranian", treatTime: ƒ}

### **Appreciation Pause**

Now, there are a lot of great people that are and have been on TC39, I would like to thank them all for their work. Doing this list has also put someone’s name in writing multiple times: [Jordan Harband](https://twitter.com/ljharb). So, I just wanted to take a quick pause to 👏👏👏👏 Jordan, who is currently on a solid [1,325 day GitHub contributions streak](https://github.com/ljharb) as of December 1, 2017. Thanks for all you do for JavaScript, Jordan!!

### **Trailing Commas**

[Proposed by: Jeff Morrison](https://github.com/tc39/proposal-trailing-function-commas)

I must admit, I think trailing commas looks super sloppy and I have never been a big fan.

let why = [
  'really?',
  'must you?',
  'yuck 😝',
]

![image alt text](image_6.gif)

That being said, I get it. I have had many occasions where I add an item to an array, a key value pair to an object, or delete an item and have had to remove or add a comma. I am one with the concept of minimizing how many keystrokes you must use. [keysleft.com](http://keysleft.com/) says I only have 213,407,968 and I just blew through 117 in this sentence alone! I've also heard the argument for the benefits this will add to checking your git diffs since you would only need to edit one line when adding function parameters, array items, etc. TBTH I'll probably take on this convention from now on. Okay, TC39? You win! 😘

### **What's to Come in 2018**

There is an awesome, emoji-laden table of proposals and what stages they are in located [here](https://github.com/tc39/proposals). You can also see the [finished proposals](https://github.com/tc39/proposals/blob/master/finished-proposals.md) including [one](https://github.com/tc39/proposal-template-literal-revision) that is already ready for 2018 publication!

Dr. Axel is here to keep you up-to-date with the happenings of ES2018: [http://2ality.com/2017/02/ecmascript-2018.html](http://2ality.com/2017/02/ecmascript-2018.html).

Usually, at this point we’re looking at Stage 4 proposals, which are proposals that will definitely be added in the next release, and Stage 3 proposals, which are proposals that have a good chance of being included in the next release.

So far, the stage 4-ers are:

* [Template Literal Revision](https://github.com/tc39/proposal-template-literal-revision) proposed by Tim Disney. Currently, the escape sequence in template literals is problematic for embedding languages like domain-specific languages. This proposal will remove the restriction on escape sequences, to understand more [click here](https://tc39.github.io/proposal-template-literal-revision/) 👆

* [s (dotAll)](https://github.com/tzmanics/blog-posts/blob/master/whitepapers/js-journey-2017)[ flag for regular expressions](https://github.com/tzmanics/blog-posts/blob/master/whitepapers/js-journey-2017) by Mathias Bynens. This proposal is all about emoji!🎈 Okay, not entirely, but it introduces the /s flag into regular expressions to make up for the dot's (.) shortcomings (like not matching with non-BMP character such as emoji). There is more to it though, so check out Mathias's [proposal](https://github.com/tc39/proposal-regexp-dotall-flag).

The list of stage 3-ers is a bit longer so I will give you [this](https://github.com/tc39/proposals#stage-3) helpful link to see the table and an image of it down below. How nice is that 😉

![image alt text](image_7.png)

## **How to JavaScript in 2017**

After discussing what changed in the standard used to create JavaScript, let’s talk about how we USE JavaScript. Last year many people, including myself, were talking about JavaScript fatigue. Yes, the ways to write a JavaScript application have not really slimmed down, BUT with a lot of command-line tools doing much of the heavy lifting, transpiling becoming less crucial and TypeScript trying to minimize type errors, we can relax a little.

![image alt text](image_8.gif)

### **Command-line Tools**

Most libraries and frameworks have a command-line tool that, with one command, will spin up skeleton projects for us to quickly create whatever our little hearts desire. This will often include a start script (sometimes with an auto re-loader), build scripts, testing structures and more. These tools are relieving us of a lot of redundant file making when we create new projects. Let's look at few more things some command line tools are taking off our plates.

#### **Webpack configurations**

Configuring your webpack build process and really understanding what you were doing, was probably one of the more daunting learning curves of 2017. Thankfully, they had one of their core contributors, [Sean Larkin](https://twitter.com/thelarkinn), running around the world supplying us with [great talks](https://www.youtube.com/watch?v=4tQiJaFzuJ8&t=3526s) and [really fun and helpful tutorials](https://www.twitch.tv/videos/209664650?t=1h57m40s).

Many frameworks nowadays not only create the webpack config files for you, but even populate them to the point that you may not even have to LOOK at it 😮 [Vue's CLI tool](https://github.com/vuejs/vue-cli) even has a [webpack-specific template](https://github.com/vuejs-templates/webpack) giving you a full-featured Webpack setup. Just to give you the full idea of what command line tools are providing, here’s what this vue cli template include, straight from the repo:

* npm run dev: first-in-class development experience.

    * Webpack + vue-loader for single file Vue components.

    * State preserving hot-reload

    * State preserving compilation error overlay

    * Lint-on-save with ESLint

    * Source maps

* npm run build: Production ready build.

    * JavaScript minified with [UglifyJS v3](https://github.com/mishoo/UglifyJS2/tree/harmony).

    * HTML minified with [html-minifier](https://github.com/kangax/html-minifier).

    * CSS across all components extracted into a single file and minified with [cssnano](https://github.com/ben-eb/cssnano).

    * Static assets compiled with version hashes for efficient long-term caching, and an auto-generated production index.html with proper URLs to these generated assets.

    * Use npm run build --reportto build with bundle size analytics.

* npm run unit: Unit tests run in [JSDOM](https://github.com/tmpvar/jsdom) with [Jest](https://facebook.github.io/jest/), or in PhantomJS with Karma + Mocha + karma-webpack.

    * Supports ES2015+ in test files.

    * Easy mocking.

* npm run e2e: End-to-end tests with [Nightwatch](http://nightwatchjs.org/).

    * Run tests in multiple browsers in parallel.

    * Works with one command out of the box:

        * Selenium and chromedriver dependencies automatically handled.

        * Automatically spawns the Selenium server.

The [preact-cli](https://github.com/developit/preact-cli#webpack), on the other hand, takes care of the standard webpack functionality. Then if you need to customize your webpack configurations you just create a preact.config.js file which exports a function that makes your webpack changes. So many tools, so much help; developers helping developers 💞.

### **Babel On or Off**

Get it? Sounds like Babylon 😂. I crack myself up. I'm not *exactly* tying Babel to the ancient city of Babylon, but there has been [talk](https://medium.freecodecamp.org/you-might-not-need-to-transpile-your-javascript-4d5e0a438ca) of possibly removing our reliance on transpiling. Babel has been a big deal for the past few years because we wanted all the shiny that ECMAScript was proposing but didn't want to wait for the browsers to catch up. With ECMAScript moving to yearly small releases browsers may be able to keep up. What is a JavaScript post without some of the awesome [kangax compatibility](https://twitter.com/kangax?lang=en) charts.

These images of these charts aren't legible because I wanted to showcase just how green they are! For full detail click the links below the images to inspect the charts further.

![image alt text](image_9.png)

[Compatability for es6](http://kangax.github.io/compat-table/es6/)

![image alt text](image_10.png)

[Compatibility for 2016+](http://kangax.github.io/compat-table/es2016plus/)

In the first graph those red chunks on the left are compilers (e.g. es-6 shim, Closure, etc.) and older browsers (i.e. Kong 4.14 and IE 11). Then the five mostly red columns on the right are the server/compilers PJS, JXA, Node 4, DUK 1.8 and DUK 2.2. On the lower graph that red section that kind of looks like a bad drawing of a dog looking at a messed up exclamation point are servers/runtimes with only Node 6.5+ having green streaks. The makeup of the left red square are the compilers/polyfils and IE 11. More importantly, LOOK AT ALL THAT GREEN! In the most popular browsers, we have practically all green. The only red mark for 2017 features is on Firefox 52 ESR for Shared Memory and Atomics.

To put some of this into perspective here are some browser usage percentages from [Wikipedia](https://en.wikipedia.org/wiki/Usage_share_of_web_browsers).

![image alt text](image_11.png)

Okay, turning off Babel may be a long ways aways because when it comes down to it we want to make a concerted effort to be accessible to as many users as we can. It is interesting to consider that we may be able to get rid of that extra step. You know, like before, when we didn't use transpilers 😆

![image alt text](image_12.gif)

### **TypeScript Talk**

If we're talking about how to JavaScript we must talk about [TypeScript](https://www.typescriptlang.org/). TypeScript came out of the Microsoft office five years ago but has been the cool kid in town 😎 in 2017. There was rarely a conference that didn't have a "Why We Love TypeScript" talk; it's like the new dev heartthrob. Without writing a sonnet to TypeScript let's talk a bit about why developers are crushing hard.

For everyone who wanted types in JavaScript, TypeScript is here to offer a strict syntactical superset of JavaScript which gives optional static typing. Pretty cool, if you're into that kind of thing. Of course, if you take a look at the newest results from the [State of JavaScript](https://stateofjs.com/2017/introduction/) survey, it seems that a lot of people ARE, in fact, into that kind of thing.

![image alt text](image_13.png)

![image alt text](image_14.gif)

To hear it straight from the source, check out this quote from Brian Terlson:

Speaking as someone who proposed types for JavaScript in 2014: I do not believe types are in the cards for the near future. This is an extremely complex problem to get right from a standards perspective. Just adopting TypeScript as the standard would of course be great for TypeScript users, but there are other typed JS supersets with pretty significant usage including closure compiler and flow. These tools all behave differently and it’s not even clear that there’s a common subset to work from (I don’t think there is in any appreciable sense). I’m not entirely sure what a standard for types looks like, and I and others will continue to investigate this as it could be very beneficial, but don’t expect anything near term - [HashNode AMA with Brian Terlson](https://hashnode.com/ama/with-brian-terlson-cj6vu9vjv01nmo1wu8vmtt1x9#cj6vuspfq01oso1wuhjo5zvd6)

#### **TypeScript ❤s Flow**

In 2017, you have probably seen many [blog posts](http://thejameskyle.com/adopting-flow-and-typescript.html) discussing the TypeScript + Flow combo. [Flow](https://flow.org/) is a static type checker for JavaScript. Flow, as you can see in the State of JavaScript survey chart list above, has about as many people interested as they do uninterested. More interesting is the stats showing how many of the people surveyed haven't heard of Flow, yet ⏰. As people learn more about Flow in 2018 maybe they will find it as beneficial as [Minko Gechev](https://twitter.com/mgechev/status/940131449025347589) does:

## ![image alt text](image_15.png)

#### **Angular ❤s TypeScript**

One may notice that all the code samples in Angular documentation are written in TypeScript. At one point, there was an option that you could choose to walk through the tutorial in JavaScript or TypeScript but it seems Angular's heart has been swayed. Looking at the chart below connecting Angular to JS flavors we can see that there is actually a tiny bit more users connecting Angular to ES6 (TypeScript: 3777, ES6: 3997). We'll see if all of this affects Angular in 2018.

![image alt text](image_16.png)

TODO: Can we add a link to Alyssa's post here

Undoubtedly, the way we JavaScript (used as a verb here) will evolve in 2018. As programmers we like to make and use tools that make our lives easier. Unfortunately, that can sometimes lead to more chaos and too many choices. Thankfully, command line tools are relieving us of some grunt work and TypeScript has satiated the type-hungry who were sick of type errors.

## **Package Manager Rumble**

Along the same lines of *how* to use JavaScript is the discussion of package managers. Modules help us utilize tooling we and other developers make because WHY would you spend time re-writing something that already exists and works well?? If that question has not popped into your head or been repeated in a team meeting at least once in 2017...you might be doing it wrong. Just sayin'.

![image alt text](image_17.gif)

Thankfully, we have teams creating better and better experiences for us to install and organize these modules. [Npm](https://github.com/npm/npm), [Yarn](https://github.com/yarnpkg/yarn) and [Bower](https://github.com/bower/bower) are still the leaders of the pack...age management tools but I also wanted to throw in [jspm](https://github.com/jspm). With close to two million installs this year, jspm is still going strong. Now this isn't going to be a package manager brawl, despite the heading of this section, I'll give you the info and you can decide what it means to you 😘 I'm not going to lie though, I use npm and like their team and what they do a ton. So, if I come across as biased, it's probably because I am.

![image alt text](image_18.gif)

### **The Digits**

Let's first take a look at the comparative installs for the year. There seems to be an almost even exponential growth between each of these package managers. npm still has a large lead over yarn but is less than double the installs of Bower. One of the first things that caught my eye is the obvious pattern of hill-like install stats. Although, jspm looks to be skimming that bottom like, it reached nearly two million installs this year.

![image alt text](image_19.png)

[https://npm-stat.com/](https://npm-stat.com/)

### ![image alt text](image_20.png)** NPM - **42,882,473 installs

It's pretty clear to see that there were many aspects of Yarn that users liked: the speed, the lockfile...

TODO: what other aspects?

😛just kidding! Although that really was my note, thank [TJ VanToll](https://twitter.com/tjvantoll) for recognizing the comedic spin. Jokes aside, Yarn got a ton of attention last year because of its Facebook backing and solutions to npm users sore spots like slow installs and errors caused by package version inconsistencies.

In response, npm released version 5, which was packed with fun things. One of the main focuses of this release was increasing their speed, which, of course, prompted amazing blog post titles like, ["npm@5 — Yarn killer?"](https://medium.com/netscape/npm-5-yarn-killer-ba69737b24d0) by Nikhil John. With this update npm is noticeable faster.

[https://twitter.com/maybekatz/status/855362606713851904](https://twitter.com/maybekatz/status/855362606713851904)

This update also included a Package.lock file which has the same benefits of the yarn.lock file, keeping your package versions consistent, and removed npm-shrinkwrap. They brought on a --save default to any package you install, which saves you those, oh-so-important keystrokes 😉. One of my favorite additions is npm’s [npx package runner](http://blog.npmjs.org/post/162869356040/introducing-npx-an-npm-package-runner). One nifty thing that npx allows you to do is use packages on a per-project basis instead of having to save packages to your machine globally. There is much more to it though, check out the awesome Kat Marchán’s [post](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) to learn more. There are also more features im general on version 5, you can check out their [blog](http://blog.npmjs.org/post/161081169345/v500) for more information.

### ![image alt text](image_21.png)** yarn - **11,154,271 installs

Even with the updates in npm 5, Yarn is still faster. Oh, you want to see the speed comparison updated on the daily? Well, Thomas Schaaf has just the thing. That's right, [here](https://docs.google.com/spreadsheets/d/1ZE5B4qJw1kNGMzjgslcWTuPYrpatzQJXSYMGNOhZ2ys/edit#gid=263077280) he has a Google doc with daily speed comparison updates.

![image alt text](image_22.png)[https://github.com/thomaschaaf/npm-vs-yarn](https://github.com/thomaschaaf/npm-vs-yarn)

Yarn is on version 1 and stays fast by caching packages and using parallel operations. Caching downloaded packages also means that you have them available whether or not you have a network connection. Yarn also focused on security using [checksums](https://www.lifewire.com/what-does-checksum-mean-2625825) (basically, the outcome of an algorithm comparing information you generate and information provided by the package to make sure they match) to verify packages before you execute its code. 

There has been some hesitance to adopt Yarn because it is a newer technology but since it’s created and backed by Facebook, it makes the choice less risky than most young technologies. Although npm seems to have nearly four times as many installs as yarn, it is important to note that yarn does not recommend installation via npm. 

Note: Installation of Yarn via npm is generally not recommended. When installing Yarn with Node-based package managers, the package is not signed, and the only integrity check performed is a basic SHA1 hash, which is a security risk when installing system-wide apps.

For these reasons, it is highly recommended that you install Yarn through the installation method best suited to your operating system.

*From the **[yarn installation guide*s](https://yarnpkg.com/en/docs/install#alternatives-tab)*.*

Tune in next year to see what happens for yarn in the year 2018, dun dun duuuuun 😋.

![image alt text](image_23.png)** Bower - **26,929,956 installs

This was a much larger number of installs than I would have ever guessed, coming in second overall and doubling yarn’s numbers. Bower is still the most popular front-end specific package manager BUT, while it is still being maintained, the Bower team is recommending users switch to using Yarn and Webpack. In October of this year, Adam Stankiewicz made a [post on the Bower blog](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) on how to migrate *off* of Bower pointing to his repo, [bower-away](https://github.com/sheerun/bower-away), that he had created in July. Yet, this year's install numbers show Bower with over double the amount of installs of Yarn, so we'll see how that goes 🤔 If you feel like cozying up for a long read, check out this [closed issue](https://github.com/bower/bower/issues/2298) discussing whether or not to deprecate Bower.

![image alt text](image_24.gif)

*I’m not sure which of these dogs I relate to more.*

One thing they may not be considering is how many users are installing Bower based on a tutorial they're following and are never actually visiting their page. Since, this message to the public is pretty recent we can take look at the numbers next year to see the impact it had.

### ![image alt text](image_25.png)**jspm.io - **1,859,116 installs

In their words "jspm is a package manager for the SystemJS universal module loader, built on top of the dynamic ES6 module loader." It can load any module format (ES6, AMD, CommonJS and globals) straight from any registry, like npm and GitHub. jspm does not seem to have much GitHub love in the form of forks and stars but there is consistent activity throughout this year. With nearly two million downloads this year and consistently staying between ~150k and 200k monthly downloads throughout the year, it seems like jspm has staying power.

![image alt text](image_26.png)

### **The Other Ones**

Okay, chunking these all together may seem harsh but, let's be honest, people aren't using them as much as npm, Bower, yarn or jspm.

*Which *other ones you may ask? Today we’re going to look at three that are currently doing the best in installs this year: [component](https://github.com/componentjs/component), [pnpm](https://github.com/pnpm/pnpm) and [ied](https://github.com/alexanderGugel/ied). If we take a look at the charts, provided by [npm stats](https://npm-stat.com/) (yes, just like yarn, these can all be installed using npm), pnpm is towering over the other two. I also wanted to show a chart looking at monthly downloads starting at February 2015. In this chart it looks as if component and ied have hit their peak and are slowly dying down whereas pnpm is on an upward trajectory. Let’s briefly dig into each project.

![image alt text](image_27.png)

![image alt text](image_28.png)

[pnpm](https://github.com/pnpm/pnpm) - 334,497 installs: By far the most installs of these "others" package management libraries and is the youngest of the bunch having its first commit in January of 2016. It focuses on speed leveraging disk space efficiency and is actively being worked on. It currently seems to be worked on actively, having a commit every few days or so.

[component](https://github.com/componentjs/component) - 35,340 installs: This project is deprecated and hasn’t had a commit in 2 years, yet still has over 35,000 installs this year.

[ied](https://github.com/alexanderGugel/ied) - 22,522 installs:  Touts being "like npm, but faster" and had its first commit back in August of 2015. It is specifically for Node, has some killer ASCII art but hasn't had a commit in over a year.

Only the future can really say what will happen to these brave "other" libraries. Although, it’s probably safe to say that component and ied may eventually fade away never to make it into the top package manager section. It *is* the open-source world though, so never say never.

So the package manager battle wages on but when it comes down to it, we have options for really great package management tools. Isn’t that the way it should be? You tell me. I’m just happy to have a great way to install all the the things I need to build all the weird app ideas I have in my head!

Related: Look at this great [list of package managers](https://github.com/topics/package-manager).

## **Conclusion**

In 2017, ECMAScript continued its small but impactful deliveries, the package manager race continues to make our experiences better, we have some great tools to make JavaScripting a tidbit easier and we have more ways to utilize the advancements of the modern web. 2017 was pretty crazy but look at all these bright spots we have in our JavaScript world. That's right, I'm an optimist! There are bound to be many more things to talk about in a year's time but, for now, let's be thankful JavaScript has survived another year without burning everything to the ground 😛

